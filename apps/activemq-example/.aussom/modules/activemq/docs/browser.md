# file: browser.aus

## class: ActiveMqBrowser

[24:14] (extern: com.lehman.aussom.ActiveMqBrowser) **extends: object** 

Walks a snapshot of a queue's messages without consuming them.
Created with ActiveMqSession.createBrowser(). Typical use:
while (b.hasMore()) { m = b.next(); }.

#### Methods

- **hasMore** ()

	> Reports whether the browse snapshot has more messages.

	- **@r** `A` bool with true while more messages are available.


- **next** ()

	> Gets the next browsed message without consuming it.

	- **@r** `An` ActiveMqMessage object.


- **getQueueName** ()

	> Gets the browsed queue's name.

	- **@r** `A` string with the queue name.


- **close** ()

	> Closes the browser. Safe to call more than once.

	- **@r** `this` object




