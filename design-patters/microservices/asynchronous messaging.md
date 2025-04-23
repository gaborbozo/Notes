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
**Dead-letter queue** is a special place in a message broker where error messages go, error such as format issues, timeouts, the queue being so backed up that it cannot accept the message.
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
* scaling the real blocking calls.

Considetarions such as
* message acknowledgment determines when the broker removes the message,
* Dead-letter queues (DLQ) should be monitored and managed properly,
* Wire time and setup overhead may outweigh benefits if the message processing is trivial.

### Publish-subscribe
Single producer - multiple consumer.

Send and forget.

In traditional pub-sub, if a subscriber isn't there, it won't get the message. However, if the **subscriber is durable**, there is a guarantee that the message will be delivered at some point once the subscriber is available again (based on this a durable subsriber must unsubsribe in order to avoid message keeping by the broker). This is a specific registration process that allows this durable subscription. Unlike point-to-point consumer can choose to listen or not listen, which allows for **dynamic expansion**.

Use cases can be
* multiple responds, f.e. a user delete event may need that a user data cleanup, logging in audit service, email revocation in a mail system, etc. need to be done,
* multiple chaining tasks, such as writing to different databases, update search indexes, trigger alerts or downstream processes, etc
## Event-driven microservices
On or more step based on an invocation from an event.
### Choreographed
Call tree, each step does some work and passes a message or the current state of an object down the change (sends data to the message broker). 

It's benefires are
* there is no centralized controller of the choreographed events,
  > Similar to _Linux_ based pipeing: `process1 | process2 | process3`
* each step can be optimized for its sole function,
* reduced reliability, lower complexity and cost.

Use cases can be
* distributed systems with independent teams react to the same event without direct coordination. Prevents tight coupling and supports diverse tools, languages, and processes,
* alternative cascades where an event may trigger multiple follow-up steps in parallel or conditionally. Choreography avoids complex and messy orchestration logic.
### Orchestrated
Events rely on a centralized orchestrator that controls the sequence of steps in a process. Since the steps are usually known in advance, the orchestrator can invoke them as needed and pull results asynchronously from services or a state store. Each step remains isolated and independent, without needing awareness of the others.

Use cases can be
* sequential processing where steps must happen in order, e.g. get credit score before approval,
* command workflows where each step depends on the previous one and messages are non-blocking,
* response aggregation when multiple steps require responses, the orchestrator collects and compiles them into a master status.

It's highly reliable, centralized error handling and improved observability, but on the other hand it performs lower than 
choreography, has higher complexity and cost due to the need for state management and robust orchestrator logic.
### Hybrid events
Combination of Choreographed and Orchestrated events.
## Stream data platform
Designed to handle continuous flows of data, typically from structured logs representing system events. It operates asynchronously and uses persistent message brokers like _Apache Kafka_, following a _pub/sub_ model with producers (e.g., applications, databases, servers) and consumers (e.g., log aggregators, analytics engines, long-term storage systems, and eventing engines).

This setup enables real-time data collection, aggregation, and analysis, supporting use cases like system monitoring, anomaly detection, and business intelligence. Despite added complexity and storage demands, stream data platforms are critical because data drives informed decisions, helps optimize resources, and ensures system reliability and responsiveness.
### Log aggregation
Two phases of log aggregation exist
* raw aggregation via the message broker (e.g., _Kafka_), which stores logs without transformations to preserve metadata,
* transformed aggregation in consumption engines, where logs are formatted for readability and analysis. This transformation tipically happens after the message broker stage, often during shipping to tools like the _Elastic ELK Stack_.

Visualization is critical to help filtering logs by metadata and improve human readibility. Also enables better operational insights, debugging, and system health checks. Essential for refactoring analysis, even in non-production environments.
### System analytics
After logs are aggregated, the next step is performing analytical exercises. While aggregation telling us what happend, the analytics will tell that why it happened.

Stream data platform is ideal for analytics because
* data from multiple services comes together (real-time context), also warehouses often requires denormalizing, optimizing queries and pre-building indexes.
  > Stream analytics lets us analyze in motion, not just after the fact.
* has no delay from ETL-ing to a warehouse,
* analytics can lead directly to automated system responses (event triggering).
## Data flows
Data is hard, necessary, and slow (due to factors like network calls, disk IO, and large index lookups). To deal with this, asynchronous messaging supports several critical patterns.
### Patterns for handling large datas
##### Distributed data & eventual consistency
> While _ACID_ (Atomicity, Consistency, Isolation, Durability) ensures strong consistency and reliability, typical of relational databases, _BASE_ (Basically Available, Soft state, Eventual consistency) prioritizes availability and resilience over immediate consistency.

Writes are made to a local database node, and the update is asynchronously propagated to other nodes. Though this increases write speed and scalability, it introduces trade-offs like **latent reads** (reading stale data from a different node) and **eventual convergence**, meaning data across nodes may not immediately align.
> Databases like Apache Cassandra manage this through quorum-based strategies, allowing control over how many replicas must confirm a write before it's acknowledged

Useful in systems with multiple or globally distributed databases. To manage risk, caching, fallback reads, global load balancing, or circuit breaker pattern may be needed to build in.
##### CQRS (Command Query Responsibility Segregation)
Improves system throughput by separating write and read models, most commonly mirroring the write database in the read database with a simpler, optimized model. Can be achieved through an event-driven asynchronous architecture where read database's service polls the message broker for the newly updated datas.

Frequently used in microservices to decouple data operations where the where the updates are frequent and expensive, or where the reads require significant transformation or aggregation of the data.
### Live data migration from monolith into microservice
Maintaining the monolithic system in operation while the new microservices architecture is developed, with the new model continuously receiving live data from the legacy system.

Reads and writes still occur in the old monolith, but the new database setup begins in parallel. The message broker handles the transport of change events while the consumer takes these events and writes to the new system. A database trigger, a service hook, or a separate process acts as the producer of change events. Every time something changes (create/update/delete), a message is sent. For most events (not delete), the consumer queries the old DB to get the current state and then calls the new service, which transforms and writes to the new DB. Some records won’t get updated naturally during the migration window so a crawler process sweeps through and “re-publishes” those records via the same messaging mechanism.
### Data synchronization between systems
Two different systems need to have the same data.

Source system, the "truth" and destination system. Producer pushes data to the message broker, often just the ID and the action. Consumer picks up the message and if the id was provided then queries the source full data, otherwise it parses the full data directly from the message. A watcher may need to be implemented which periodically scans both systems and compares state between the source and destination to find mistmatch. It assuemes source is correct and pushes an update via the producer to re-sync.

<!--stackedit_data:
eyJoaXN0b3J5IjpbMjkwMTIxNTEzLC0xNDAzMTkxMzgxLC0yMD
I1NDE5NzIzLDIxMTUyODk1ODMsLTI3NDgyNTA1MSw4OTA3Nzgx
NjcsLTExMjUwNTE4NzgsLTE1NzI4OTA1MTEsMTExOTE1MDkxMC
w0NDE1MDYwNjQsLTM0ODg3ODY3NSwxMTY3OTM2MzgwLC0xMzE2
NTA2ODkzLC0xNTA2MDI2NDY1LDY3Mjk3NTA5MSwxMzE0MjA4Nj
EyLDEyNDkwMTkwMDMsNTc0MTAzMDEzLDQyNzMyOTUwMywtMTk2
NzI0ODEzNl19
-->