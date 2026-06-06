# file: consumer.aus

## class: ActiveMqConsumer

[26:14] (extern: com.lehman.aussom.ActiveMqConsumer) **extends: object** 

Pulls messages from a destination. Created with
ActiveMqSession.createConsumer() or createDurableSubscriber().
Consumption here is synchronous (receive); push-style consumption
runs through ActiveMqListener under the Aussom Server listener
runtime.

#### Methods

- **receive** (`int TimeoutMs = 0`)

	> Receives the next message, waiting up to TimeoutMs. A timeout of 0 waits forever.

	- **@p** `TimeoutMs` is an int with the wait in milliseconds (default 0).
	- **@r** `An` ActiveMqMessage object, or null when the timeout expires.


- **receiveNoWait** ()

	> Returns the next message only if one is ready right now.

	- **@r** `An` ActiveMqMessage object, or null when none is ready.


- **getSelector** ()

	> Gets this consumer's JMS selector.

	- **@r** `A` string with the selector, or null when none is set.


- **close** ()

	> Closes the consumer. Safe to call more than once.

	- **@r** `this` object




