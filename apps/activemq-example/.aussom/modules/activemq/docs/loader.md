# file: loader.aus

## class: activemq_module

[26:14] `static` **extends: object** 

Loader for the activemq module. Every other activemq `.aus` file
includes it at the top so `aussom-activemq.jar` is on the classpath
before any extern class in this module resolves. The include is
deduped by path, so the loadJar call runs exactly once per process
no matter how many activemq files include it.

#### Methods

- **activemq\_module** ()




