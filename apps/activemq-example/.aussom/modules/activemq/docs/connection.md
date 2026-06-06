# file: connection.aus

## class: ActiveMqConnection

[27:14] (extern: com.lehman.aussom.ActiveMqConnection) **extends: object** 

Connection to an ActiveMQ broker. The URL decides the mode: a
vm:// URL reaches an embedded ActiveMqBroker in this JVM, while
tcp://host:61616 or failover:(tcp://a:61616,tcp://b:61616) reach
an outside broker. Configuration setters apply at connect() time,
so call them first.

#### Methods

- **ActiveMqConnection** (`string BrokerUrl, string User = null, string Password = null`)

	> Creates a connection definition. Nothing touches the network until connect() is called.

	- **@p** `BrokerUrl` is a string with the broker URL.
	- **@p** `User` is a string with the user name (optional).
	- **@p** `Password` is a string with the password (optional).


- **newConnection** (`string BrokerUrl, string User = null, string Password = null`)


- **setClientId** (`string Id`)

	> Sets the JMS client ID. Required before creating durable topic subscriptions. Call before connect().

	- **@p** `Id` is a string with the client ID.
	- **@r** `this` object


- **setPrefetch** (`int Count`)

	> Sets the prefetch count for all destination types. Lower values spread messages across competing consumers; higher values favor throughput. Call before connect().

	- **@p** `Count` is an int with the prefetch count.
	- **@r** `this` object


- **setRedeliveryPolicy** (`int MaxRedeliveries, int InitialDelayMs = 1000, double Multiplier = 1.0, bool UseExponentialBackOff = false`)

	> Configures client-side redelivery after rollback or recover. Call before connect().

	- **@p** `MaxRedeliveries` is an int with the redelivery cap (-1 for unlimited).
	- **@p** `InitialDelayMs` is an int with the first redelivery delay (default 1000).
	- **@p** `Multiplier` is a double applied to the delay each attempt (default 1.0).
	- **@p** `UseExponentialBackOff` is a bool enabling the multiplier (default false).
	- **@r** `this` object


- **setTrustedPackages** (`list Packages`)

	> Sets the package allowlist for object message deserialization. Without this call no packages are trusted and reading an object message body fails. Call before connect().

	- **@p** `Packages` is a list of package name strings (for example ['java.util', 'java.lang']).
	- **@r** `this` object


- **setUseAsyncSend** (`bool On`)

	> Enables fire-and-forget sends for higher producer throughput at the cost of delivery guarantees. Call before connect().

	- **@p** `On` is a bool with true to enable async sends.
	- **@r** `this` object


- **connect** ()

	> Connects to the broker and starts inbound message delivery.

	- **@r** `this` object


- **start** ()

	> Resumes inbound message delivery after stop().

	- **@r** `this` object


- **stop** ()

	> Pauses inbound message delivery without closing the connection. Producers keep working while stopped.

	- **@r** `this` object


- **createSession** (`bool Transacted = false, string AckMode = "auto"`)

	> Creates a session. A transacted session ignores the acknowledge mode and batches work until commit() or rollback().

	- **@p** `Transacted` is a bool with true for a transacted session (default false).
	- **@p** `AckMode` is a string with auto, client, dups_ok, or individual (default auto).
	- **@r** `A` new ActiveMqSession object.


- **close** ()

	> Closes the connection and every session, producer, and consumer created from it. Safe to call more than once.

	- **@r** `this` object


- **isConnected** ()

	> Reports whether the connection is open.

	- **@r** `A` bool with true while connected.


- **getBrokerUrl** ()

	> Gets the broker URL this connection targets.

	- **@r** `A` string with the broker URL.




