# file: producer.aus

## class: ActiveMqProducer

[24:14] (extern: com.lehman.aussom.ActiveMqProducer) **extends: object** 

Sends messages to a destination. Created with
ActiveMqSession.createProducer(). Producers bound to a destination
use send(); anonymous producers (created with null) use sendTo().

#### Methods

- **setDeliveryMode** (`string Mode`)

	> Sets the default delivery mode for sends.

	- **@p** `Mode` is a string with persistent or non_persistent.
	- **@r** `this` object


- **setPriority** (`int P`)

	> Sets the default priority for sends.

	- **@p** `P` is an int from 0 to 9 (the JMS default is 4).
	- **@r** `this` object


- **setTimeToLive** (`int Ms`)

	> Sets the default time-to-live for sends.

	- **@p** `Ms` is an int with milliseconds, 0 for never expire.
	- **@r** `this` object


- **setDisableMessageId** (`bool On`)

	> Skips message ID generation for a small performance gain.

	- **@p** `On` is a bool with true to skip IDs.
	- **@r** `this` object


- **setDisableMessageTimestamp** (`bool On`)

	> Skips timestamp generation for a small performance gain.

	- **@p** `On` is a bool with true to skip timestamps.
	- **@r** `this` object


- **send** (`object Msg, DeliveryMode = null, Priority = null, TtlMs = null`)

	> Sends a message to this producer's destination. The optional arguments override the producer defaults for this send only.

	- **@p** `Msg` is an ActiveMqMessage object.
	- **@p** `DeliveryMode` is a string with persistent or non_persistent (optional).
	- **@p** `Priority` is an int from 0 to 9 (optional).
	- **@p** `TtlMs` is an int with the time-to-live in milliseconds (optional).
	- **@r** `this` object


- **sendTo** (`object Dest, object Msg`)

	> Sends a message to an explicit destination from an anonymous producer. This is how request/reply consumers answer to a message's replyTo.

	- **@p** `Dest` is an ActiveMqDestination object.
	- **@p** `Msg` is an ActiveMqMessage object.
	- **@r** `this` object


- **close** ()

	> Closes the producer. Safe to call more than once.

	- **@r** `this` object




