# file: destination.aus

## class: ActiveMqDestination

[24:14] (extern: com.lehman.aussom.ActiveMqDestination) **extends: object** 

A queue or topic, including the temporary variants. Instances come
from ActiveMqSession's create methods and from message replyTo /
destination headers - there is no public constructor.

#### Methods

- **getName** ()

	> Gets the queue or topic name.

	- **@r** `A` string with the destination name.


- **isQueue** ()

	> Reports whether this destination is a queue.

	- **@r** `A` bool with true for a queue.


- **isTopic** ()

	> Reports whether this destination is a topic.

	- **@r** `A` bool with true for a topic.


- **isTemporary** ()

	> Reports whether this destination is temporary.

	- **@r** `A` bool with true for a temporary queue or topic.


- **delete** ()

	> Deletes a temporary destination. Errors on non-temporary ones.

	- **@r** `this` object




