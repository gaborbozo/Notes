# Asynchronous messaging
Traditional concept is a synchronous  blocking call over _HTTP_ using _REST_-ful patterns.

> **Gridlock** refers to a situation where services are waiting on each other in a circular or deadlocked way, causing the whole system (or parts of it) to freeze or stall.

On the other hand asynchronous methology works like 
1. Over **_HTTP_ using _REST_** the client sends a call and the server immediately reponds with an accepted status code. The client then either polls the server or waits for a push message on a callback _URL_ to determine if the work was done and successful or done and failed.
2. Using a **messaging system** like RabbitMQ, Kafka, JMS or others. A message is put on a system and a downstream consumer works on that message. Successes or failures can be communicated many different ways or not at all in these various patterns.
## Message broker
Heart of the system. Translates message from one system into a message for another system. Ensures reliable delivery even if the sender and receiver aren't active at the same time.

Routing can range from simple point-to-point to complex message inspection and fan-out. A message broker handles this, ensuring consumers only receive relevant messages. It can also split or combine messages as needed for efficient delivery. 

These components are a great source for handling and responding errors.

RabbitMQ, Apache ActiveMQ, Java Message Services, Apache Kafka, Cache.
## Terms
**Producer** creates message for another system to act on. It builds the message in the correct format (based on a contract) and dispatches it to the message broker. Once the message is sent, the producer usually confirms acceptance and ends the process.
**Consumer** (or receiver) is the system that receives messages from the message broker. While there are various ways this can happen, the core responsibility of the consumer is to act on the message. After processing, it may either do nothing further (in simple workflows), or it may send a new message — either to another system downstream or back to the original sender, often as a response or callback.
**Dead-letter queue** is a special palce in a message broker where error messages go, error such as format issues, timeouts, the queue being so backed up that it cannot accept the message.
## Interservice communication patterns
### Point-to-point
These calls can replace traditional restful calls between services, where the response is not needed or can be received in and out of band process. 

Single producer creates a message and puts it into the message broker. Single consumer responds or listens (polls) to the message and does some action on it.

**Send and forget** means that after the producer creates the message, it dispatches the message, and goes on.

Any kind of reponse is usually another point-to-point 
message.

It is used when
* no response needed, f.e. audit records,
* admin tasks such as clean up processes,
* out of band processes, f.e. email sending,
* scaling the real blocking calls

Considetarions such as
* message acknowledgment determines when the broker removes the message,
* Dead-letter queues (DLQ) should be monitored and managed properly,
* Wire time and setup overhead may outweigh benefits if the message processing is trivial

### Publish-subscribe
Single producer - multiple consumer.

Send and forget.

In traditional pub-sub, if a subscriber isn't there, it won't get the message. However, if the **subscriber is durable**, there is a guarantee that the message will be delivered at some point once the subscriber is available again (based on this a durable subsriber must unsubsribe in order to avoid message keep). This is a specific registration process that allows this durable subscription. Unlike point-to-point consumer can choose to listen or not listen, which allows for **dynamic expansion**.

Use cases can be
* multiple responds,
* multiple tasks
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE1NzUwMTk2MzQsNDI3MzI5NTAzLC0xOT
Y3MjQ4MTM2LDE1NDM1MDM5NzQsLTE0NDAxNTc0MzEsLTE5NDMz
NDc0OTYsLTEzMzgwMDU4ODgsNzA3MjcyNzQ1LC00NDA1NzUxNj
YsLTIwNjcyNzUzNzhdfQ==
-->