# activemq

Apache ActiveMQ Classic connector for Aussom. One module covers both
modes: an embedded broker running inside your JVM (entirely in memory
or persisting to disk) and connections to an outside ActiveMQ server.
The broker URL decides which one you get.

Built on ActiveMQ Classic 6.2.x (Jakarta JMS).

## Classes

| Class | Purpose |
|---|---|
| `ActiveMqBroker` | Embedded broker: in-memory or KahaDB persistence, vm:// and TCP connectors |
| `ActiveMqConnection` | Connection to an embedded (`vm://`) or remote (`tcp://`, `failover:`) broker |
| `ActiveMqSession` | Sessions, transactions, destinations, message factories |
| `ActiveMqDestination` | Queues, topics, temporary destinations |
| `ActiveMqProducer` | Sending, delivery mode / priority / TTL |
| `ActiveMqConsumer` | Synchronous receiving, selectors |
| `ActiveMqBrowser` | Queue browsing without consuming |
| `ActiveMqMessage` | All five JMS message types, headers, properties, scheduled delivery |
| `ActiveMqListener` | Aussom Server `ClientListener` connector: push-style consumption on a server-managed thread |

`include activemq.activemq;` pulls in everything; individual files can
be included instead (for example `include activemq.broker;`).

## Quick start: embedded, in memory

```aussom
include activemq.activemq;

broker = new ActiveMqBroker("mybroker");
broker.start();

con = new ActiveMqConnection(broker.getVmUrl());
con.connect();
sess = con.createSession();

q = sess.createQueue("orders");
prod = sess.createProducer(q);
prod.send(sess.createTextMessage("hello"));

cons = sess.createConsumer(q);
m = cons.receive(5000);
c.println(m.getText());    // hello

con.close();
broker.stop();
```

## Embedded with disk persistence

The data directory must live inside the app's `app_data` directory.
Under Aussom Server the path is resolved and checked by the server's
file rules; messages sent with the (default) persistent delivery mode
survive a broker restart.

```aussom
broker = new ActiveMqBroker("mybroker");
broker.setPersistent(true);
broker.setDataDirectory("app_data/activemq");
broker.start();
```

## Connecting to an outside ActiveMQ server

```aussom
con = new ActiveMqConnection("failover:(tcp://mq1:61616,tcp://mq2:61616)", "user", "pass");
con.connect();
```

An embedded broker can also accept outside clients:

```aussom
broker.addConnector("tcp://0.0.0.0:61616");   // before start()
```

## Feature notes

- **Ack modes**: `auto` (default), `client`, `dups_ok`, and ActiveMQ's
  `individual` via `createSession(false, "client")` etc. Transacted
  sessions via `createSession(true)` with `commit()` / `rollback()`.
- **Durable topic subscriptions**: set a client ID on the connection
  first (`setClientId`), then `createDurableSubscriber(topic, name)`.
- **Request/reply**: `createTemporaryQueue()` + `setReplyTo` +
  `setCorrelationId`; the service side replies with an anonymous
  producer's `sendTo(msg.getReplyTo(), reply)`.
- **Scheduled delivery**: enable `setSchedulerSupport(true)` on the
  broker, then `msg.setScheduledDelay(ms)` (or period/repeat/cron).
- **Object messages**: deserialization is off by default. Allowlist
  packages with `con.setTrustedPackages(["java.lang", "java.util"])`
  before connecting.
- **Wildcards / composite destinations**: ActiveMQ names like
  `orders.>` or `a,b` are plain strings and work unchanged.

## Building and testing

```
mvn clean package
```

Tests are fully self-contained: the aunit suite (`activemq-test.aus`)
runs against an embedded in-memory broker, including a real TCP
round trip through a connector on a free port and a KahaDB
persistence-across-restart check (written under `./app_data/`,
which is gitignored).

## Server listener

Under Aussom Server, `ActiveMqListener` is the push-consumption
path. Register it and the server runtime owns its lifecycle: a
dedicated thread, reload/shutdown handling, and the auto-restart
policy from `applications.yaml` (keyed by the listener name).

```aussom
include app;
include activemq.activemq;

class orders : AppBase {
    private broker = null;

    public orders() {
        this.broker = new ActiveMqBroker("orders");
        this.broker.setPersistent(true);
        this.broker.setDataDirectory("app_data/activemq");
        this.broker.start();

        lst = new ActiveMqListener("orders.created");
        lst.setBrokerUrl(this.broker.getVmUrl());
        lst.setQueue("orders.created");
        lst.setAckMode("individual");
        lst.setOnMessage(::onOrder);
        app.registerListener(lst);
    }

    public onOrder(object Msg) {
        console.info("got order: " + Msg.getText());
        Msg.ack();
    }
}
```

Handlers run on the listener thread, so slow handlers apply natural
back-pressure. A handler error never kills the receive loop: with
`client`/`individual`/`transacted` ack modes the message is
redelivered by default (`setRedeliverOnError(false)` to ack anyway),
and an optional `setOnError` callback receives the error text.
Outside the server (plain CLI, tests) the loop can be driven
directly: `startListener()` blocks (run it on a `Thread`),
`stopListener()` ends it.
