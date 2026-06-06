# file: message.aus

## class: ActiveMqMessage

[26:14] (extern: com.lehman.aussom.ActiveMqMessage) **extends: object** 

One wrapper for every JMS message type: text, bytes, map, stream,
object, and the body-less base message. Headers and properties are
shared by all types; the body methods error cleanly when called on
the wrong type. Instances come from the ActiveMqSession create*
methods and from receive() - there is no public constructor.

#### Methods

- **getMessageType** ()

	> Gets this message's type.

	- **@r** `A` string with text, bytes, map, stream, object, or message.


- **getText** ()

	> Gets the body of a text message.

	- **@r** `A` string with the body, or null when unset.


- **setText** (`string Text`)

	> Sets the body of a text message.

	- **@p** `Text` is a string with the body.
	- **@r** `this` object


- **writeBytes** (`object Buff`)

	> Appends the contents of a Buffer to a bytes message.

	- **@p** `Buff` is a Buffer object with the bytes to append.
	- **@r** `this` object


- **readBytes** ()

	> Reads the full body of a bytes message.

	- **@r** `A` Buffer object with the body bytes.


- **setMapValue** (`string Name, Value`)

	> Sets a named value on a map message. Strings, ints, doubles, bools, and Buffers are supported.

	- **@p** `Name` is a string with the value name.
	- **@p** `Value` is the value to store.
	- **@r** `this` object


- **getMapValue** (`string Name`)

	> Reads a named value from a map message.

	- **@p** `Name` is a string with the value name.
	- **@r** `The` stored value, or null when the name is missing.


- **getMapNames** ()

	> Lists the names present in a map message.

	- **@r** `A` list of strings with the value names.


- **writeValue** (`Value`)

	> Appends a value to a stream message. Strings, ints, doubles, bools, and Buffers are supported.

	- **@p** `Value` is the value to append.
	- **@r** `this` object


- **readValue** ()

	> Reads the next value from a stream message, starting from the beginning on a freshly written message.

	- **@r** `The` next value in the stream.


- **setObject** (`Value`)

	> Sets the payload of an object message. Strings, ints, doubles, bools, lists, and maps convert to serializable Java values.

	- **@p** `Value` is the payload.
	- **@r** `this` object


- **getObject** ()

	> Reads the payload of an object message. The connection must trust the payload's packages (setTrustedPackages).

	- **@r** `The` payload value.


- **getCorrelationId** ()

	> Gets the correlation ID used to pair replies with requests.

	- **@r** `A` string with the correlation ID, or null when unset.


- **setCorrelationId** (`string Id`)

	> Sets the correlation ID used to pair replies with requests.

	- **@p** `Id` is a string with the correlation ID.
	- **@r** `this` object


- **getReplyTo** ()

	> Gets the destination replies should be sent to.

	- **@r** `An` ActiveMqDestination object, or null when unset.


- **setReplyTo** (`object Dest`)

	> Sets the destination replies should be sent to.

	- **@p** `Dest` is an ActiveMqDestination object.
	- **@r** `this` object


- **getType** ()

	> Gets the application-set JMS type header.

	- **@r** `A` string with the type, or null when unset.


- **setType** (`string Type`)

	> Sets the application JMS type header.

	- **@p** `Type` is a string with the type.
	- **@r** `this` object


- **getMessageId** ()

	> Gets the broker-assigned message ID (set after send).

	- **@r** `A` string with the message ID, or null before send.


- **getTimestamp** ()

	> Gets the send timestamp (set after send).

	- **@r** `An` int with milliseconds since the epoch.


- **getDestination** ()

	> Gets the destination this message was sent to.

	- **@r** `An` ActiveMqDestination object, or null before send.


- **getDeliveryMode** ()

	> Gets this message's delivery mode.

	- **@r** `A` string with persistent or non_persistent.


- **getPriority** ()

	> Gets this message's priority.

	- **@r** `An` int from 0 to 9.


- **getExpiration** ()

	> Gets the expiration timestamp.

	- **@r** `An` int with milliseconds since the epoch, 0 for never.


- **getRedelivered** ()

	> Reports whether the broker redelivered this message.

	- **@r** `A` bool with true for a redelivered message.


- **setProperty** (`string Name, Value`)

	> Sets a typed property. The JMS property type follows the value type: string, int, double, or bool.

	- **@p** `Name` is a string with the property name.
	- **@p** `Value` is the property value.
	- **@r** `this` object


- **getProperty** (`string Name`)

	> Reads a property by name.

	- **@p** `Name` is a string with the property name.
	- **@r** `The` property value, or null when missing.


- **getPropertyNames** ()

	> Lists this message's property names.

	- **@r** `A` list of strings with the property names.


- **hasProperty** (`string Name`)

	> Reports whether a property exists.

	- **@p** `Name` is a string with the property name.
	- **@r** `A` bool with true when the property exists.


- **setScheduledDelay** (`int Ms`)

	> Delays delivery. The broker needs scheduler support enabled.

	- **@p** `Ms` is an int with the delay in milliseconds.
	- **@r** `this` object


- **setScheduledPeriod** (`int Ms`)

	> Redelivers every period (with setScheduledRepeat). The broker needs scheduler support enabled.

	- **@p** `Ms` is an int with the period in milliseconds.
	- **@r** `this` object


- **setScheduledRepeat** (`int Count`)

	> Sets how many times a periodic delivery repeats.

	- **@p** `Count` is an int with the repeat count.
	- **@r** `this` object


- **setScheduledCron** (`string Expr`)

	> Schedules delivery with a cron expression. The broker needs scheduler support enabled.

	- **@p** `Expr` is a string with the cron expression.
	- **@r** `this` object


- **ack** ()

	> Acknowledges this message on a client or individual acknowledge session.

	- **@r** `this` object




