# file: session.aus

## class: ActiveMqSession

[30:14] (extern: com.lehman.aussom.ActiveMqSession) **extends: object** 

A JMS session created from ActiveMqConnection.createSession().
Destinations, producers, consumers, browsers, and messages are all
created here, and transactions commit or roll back here. Use one
session per thread, per the JMS contract.

#### Methods

- **createQueue** (`string Name`)

	> Gets a queue destination. ActiveMQ wildcard names (orders.>) and composite names (a,b) are plain strings and work unchanged.

	- **@p** `Name` is a string with the queue name.
	- **@r** `A` new ActiveMqDestination object.


- **createTopic** (`string Name`)

	> Gets a topic destination.

	- **@p** `Name` is a string with the topic name.
	- **@r** `A` new ActiveMqDestination object.


- **createTemporaryQueue** ()

	> Creates a temporary queue that lives as long as the connection. Useful as a private reply destination for request/reply.

	- **@r** `A` new ActiveMqDestination object.


- **createTemporaryTopic** ()

	> Creates a temporary topic that lives as long as the connection.

	- **@r** `A` new ActiveMqDestination object.


- **createProducer** (`object Dest = null`)

	> Creates a producer. With a destination the producer's send() targets it; with null the producer is anonymous and sendTo() picks the destination per message.

	- **@p** `Dest` is an ActiveMqDestination object or null (default null).
	- **@r** `A` new ActiveMqProducer object.


- **createConsumer** (`object Dest, string Selector = null, bool NoLocal = false`)

	> Creates a consumer on a destination.

	- **@p** `Dest` is an ActiveMqDestination object.
	- **@p** `Selector` is a string with a JMS selector, or null (default null).
	- **@p** `NoLocal` is a bool that skips messages sent on this connection - topics only (default false).
	- **@r** `A` new ActiveMqConsumer object.


- **createDurableSubscriber** (`object Topic, string SubName, string Selector = null, bool NoLocal = false`)

	> Creates a durable topic subscription. The connection needs a client ID (setClientId) set before connect(). Messages published while the subscriber is offline wait for it.

	- **@p** `Topic` is an ActiveMqDestination topic object.
	- **@p** `SubName` is a string with the subscription name.
	- **@p** `Selector` is a string with a JMS selector, or null (default null).
	- **@p** `NoLocal` is a bool that skips messages sent on this connection (default false).
	- **@r** `A` new ActiveMqConsumer object.


- **unsubscribe** (`string SubName`)

	> Removes a durable subscription by name. Close its consumer first.

	- **@p** `SubName` is a string with the subscription name.
	- **@r** `this` object


- **createBrowser** (`object Queue, string Selector = null`)

	> Creates a browser that walks a snapshot of a queue without consuming its messages.

	- **@p** `Queue` is an ActiveMqDestination queue object.
	- **@p** `Selector` is a string with a JMS selector, or null (default null).
	- **@r** `A` new ActiveMqBrowser object.


- **createTextMessage** (`string Text = null`)

	> Creates a text message.

	- **@p** `Text` is a string with the initial body, or null (default null).
	- **@r** `A` new ActiveMqMessage object.


- **createBytesMessage** ()

	> Creates an empty bytes message. Fill it with writeBytes().

	- **@r** `A` new ActiveMqMessage object.


- **createMapMessage** ()

	> Creates an empty map message. Fill it with setMapValue().

	- **@r** `A` new ActiveMqMessage object.


- **createStreamMessage** ()

	> Creates an empty stream message. Fill it with writeValue().

	- **@r** `A` new ActiveMqMessage object.


- **createObjectMessage** ()

	> Creates an object message. Set the payload with setObject(). Reading the payload back requires trusted packages on the connection.

	- **@r** `A` new ActiveMqMessage object.


- **createMessage** ()

	> Creates a body-less message carrying only headers and properties.

	- **@r** `A` new ActiveMqMessage object.


- **commit** ()

	> Commits all sends and receives since the last commit on a transacted session.

	- **@r** `this` object


- **rollback** ()

	> Rolls back all sends and receives since the last commit on a transacted session. Received messages are redelivered.

	- **@r** `this` object


- **recover** ()

	> Redelivers messages received but not yet acknowledged on a client or individual acknowledge session.

	- **@r** `this` object


- **getTransacted** ()

	> Reports whether this session is transacted.

	- **@r** `A` bool with true for a transacted session.


- **getAckMode** ()

	> Gets this session's acknowledge mode.

	- **@r** `A` string with auto, client, dups_ok, individual, or transacted.


- **close** ()

	> Closes the session and everything created from it. Safe to call more than once.

	- **@r** `this` object




