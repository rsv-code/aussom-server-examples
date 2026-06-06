# file: broker.aus

## class: ActiveMqBroker

[31:14] (extern: com.lehman.aussom.ActiveMqBroker) **extends: object** 

Embedded ActiveMQ broker. Runs entirely in memory by default; call
setPersistent(true) and setDataDirectory() to keep messages in a
KahaDB store on disk. Clients in this JVM connect with getVmUrl();
addConnector() opens TCP ports for outside clients.
If a broker with the same name is already running in this JVM (for
example after an app hot reload), start() attaches to it instead of
starting a second instance, and configuration setters are ignored
with a logged warning. stop() stops the shared instance.

#### Methods

- **ActiveMqBroker** (`string Name`)

	> Creates a broker with the provided name. The name is also the vm:// address clients in this JVM use.

	- **@p** `Name` is a string with the broker name.


- **newBroker** (`string Name`)


- **setPersistent** (`bool Persistent`)

	> Enables or disables disk persistence (KahaDB). Default false, meaning the broker runs entirely in memory. With persistence on, call setDataDirectory() before start().

	- **@p** `Persistent` is a bool with true to write messages to disk.
	- **@r** `this` object


- **setDataDirectory** (`string Dir`)

	> Sets the directory the broker writes its files to. The directory must be inside the app's app_data directory (for example 'app_data/activemq'); under Aussom Server the path is resolved and checked by the server's file rules.

	- **@p** `Dir` is a string with the app_data-relative directory.
	- **@r** `this` object


- **\_setDataDirectoryResolved** (`string Dir, string AbsPath`)


- **setSchedulerSupport** (`bool On`)

	> Enables broker-side scheduled message delivery (used by the ActiveMqMessage setScheduled* methods). In-memory brokers keep scheduled jobs in memory; persistent brokers store them under the data directory.

	- **@p** `On` is a bool with true to enable the scheduler.
	- **@r** `this` object


- **setAdvisorySupport** (`bool On`)

	> Enables or disables advisory topics. Default true, matching ActiveMQ's own default.

	- **@p** `On` is a bool with true to enable advisory topics.
	- **@r** `this` object


- **setMemoryLimitMb** (`int Mb`)

	> Caps the broker's message memory usage. 0 leaves the ActiveMQ default in place.

	- **@p** `Mb` is an int with the memory limit in megabytes.
	- **@r** `this` object


- **addConnector** (`string Url`)

	> Adds a transport connector opened at start(), for example 'tcp://127.0.0.1:0' (port 0 picks a free port; read the real one with getConnectorUrls()). Call before start().

	- **@p** `Url` is a string with the connector URI.
	- **@r** `this` object


- **start** ()

	> Starts the broker, or attaches to an already-running broker with the same name (see class docs).

	- **@r** `this` object


- **stop** ()

	> Stops the broker. Safe to call more than once. This stops the shared JVM-wide instance, including an attached one.

	- **@r** `this` object


- **isStarted** ()

	> Reports whether the broker is running.

	- **@r** `A` bool with true while the broker is started.


- **getBrokerName** ()

	> Gets the broker name.

	- **@r** `A` string with the broker name.


- **getVmUrl** ()

	> Gets the vm:// URL clients in this JVM connect with.

	- **@r** `A` string with the vm:// connection URL.


- **isAdopted** ()

	> Reports whether start() attached to an already-running broker instead of starting a new one.

	- **@r** `A` bool with true when the broker was adopted.


- **getConnectorUrls** ()

	> Gets the actual bound transport connector URIs. A port 0 connector shows its real port here.

	- **@r** `A` list of strings with the connector URIs.




