# Microservices history
Tight coupling of components in monoliths make changes hard, thus they require considerable time to test, build and deploy.

After this there was a shift to service-based architectures (_SOA_), which decomposed applications into smaller modules. It brought other issues such as
* _SOAP_ which makes a lot of compromises that are contrary to how _HTTP_ works, f.e. ignores _HTTP_ response codes except _OK (200)_ and _Internal Server Error (500)_ - the actual error is burried inside the `<soap:Fault>` so the client can’t just use the HTTP status code.
* the aggregation layer got tightly coupled to domain-, data access- and presentation layer logics.

Microservices also have their of set of problems, but they do however <u>have the promise of a more agile framework that can be extended into a cloud native world</u> much easire than its peers before.
# Microservices and cloud-native
Cloud native includes patterns for designing systems to run in a cloud-based infrastrucutre. Cloud computing is a pattern of globally distributing systems to provide increased uptime, increased scalability and increased distribution. 

Microservices tends to fit good in this concept, however in reality they differ, but in generally every microservice based application is aimed to a cloud native platform.
# Concept of microservices 
Using the concepts of _decomposition_, breaking a software problem into smaller pieces.
It embraces the concepts of protocol aware so traditionally it's using _REST_ for communicating.
**Polyglot** development support - multiple programming languages in the same enviroment.
In a **pure** microservice architecture each unit of work can be called from any other unit of work.
Because of distribution a microservice is scalable under heavy load with not just vertiacal scaling, but with horizontal scaling as well. 
### The cost to pay
Contrary to a monolith its more complex and costfull. 
Network's distribution tax comes from thread blocking between services.
With the increase of services it gets less reliable, f.e. if one service is faulty, some other services will be too.
> If a system cannot work in a partial state of availability, it may not be developed with microservice arhitecture.

To overcome this issue a solid versioning strategy and contract testing may be helpful.

Because of the design, every service call is a remote network call, thus there is a connection set up, tear down, and wire latency. **Gridlock** happens when the delay can become unbearable, even by circuit calls. On such pattern is to use a **circuit breaker**. What it does is that if a request takes too long to be processed, a default response is returned. 
> For example Netflix released Hystrix to support their offerings. If search is down, for instance, the platform should still be able to allow users to view movies.
## Bounded context
The instinct might be to simply split a monolithic system based on data domains, but doing so without deeper analysis can lead to increased latency. It's important to take the time to understand real-world usage and analyze traffic patterns in code.
## Transactional boundaries
For this the overall objective is to minimize the cross-domain calls where possible, enforce the needed transaction boundaries. Usually moving to microservices from monolith, the data domain distribution is the last thing to do so.

> Atomicity: All operations in a transaction succeed or none do.
> Consistency: The database remains in a valid state before and after the transaction.
> Isolation: Concurrent transactions don’t interfere with each other. 
> Durability: Once a transaction is committed, it stays committed—even after a crash.
> 
Instead of _ACID_, only **BASE** (basically available). We aim for a situation where, assuming the data isn't modified again, we will achieve the end state in all of the nodes across our distributed data store.
## API layer
Forwarding requests without altering them - transformation should be handled elsewhere.

Clients interact with a unified interface, not with individual microservices directly, this decouples clients from internal changes, which makes it easier to scale services independently and handle infrastructure changes (like changing IPs, ports, or data centers) without impacting clients.
## Asynchronous communication
Strategy for dealing with reducing latency on a microservices based system is to not rely on a purely synchronous communication model.

Most often is is reffered to event-driven microservices as a way to support eventual consistency of the data.
> For example a message service put data into an asynchronous message broker (message queue) or a temporary data store, and then drive events from this state change.
> Another example is a stream data platform, where events are written to a central message broker. These events then trigger listener operations that take action on the data if it applies to them, events such as data formatting, downstream event, etc.

It is important to take care of error states correctly and recover from them.
## CI/CD as foundation
Automated deployment is crucial. Goal is maximal automation to ensure safe, reliable, and fast delivery. Without automating delivery, microservices don't truly offer agility.

Start small with basic build and deploy automation, and gradually integrate with ticketing, chat, and monitoring systems. Over time, aim for advanced automation, including self-registration and smart routing, to fully realize the benefits of microservices agility.
# Design considerations
1. CI/CD first
Model a sample pipeline and automate critical steps of the SDLC.
2. Centralized logging, tracing & telemetry
Common library for logging, tracing, and telemetry.
Plan early for log aggregation and search mechanisms.
3. Domain-driven design (DDD)
Analyze the whole system to define clear service boundaries.
Use telemetry to inform these boundaries.
4. Service design strategy
Decide between dedicated data services vs. integrating data access into business processes.
Plan for asset transactions vs. eventual consistency.
5. Latency management
Include mechanisms to measure and control latency.
Use non-blocking code where appropriate.
6. Standardize stack
Pick and enforce coding standards across all services.
Standardization eases team collaboration and resource shifting.
7. Asynchronous by default
Design services as asynchronous unless synchrony is proven necessary.
Helps reduce system latency and error rates, and builds async proficiency.
8. Focus on Operations and Infrastructure
Emphasize the supporting processes and environment, not just the code itself.
# Hybrid architectures for microservices adoption
## Hierarchical Service Model
Based on the _N-tier_ architecture.
Services are organized into distinct layers or classes like
- data services expose domain-specific logic,
- business process services define high-level workflows,
- gateway services manage external dependencies,
- edge services expose functionality externally.

Strict consumption rules are defined between layers (e.g., no data service calls another directly).

Pros: 
- Reduces risk of circular dependencies.
- Helps manage complexity during monolith to microservices migration. 

Cons:
- Can force unnecessary business logic and pass-through services.
- May introduce artificial complexity and latency.
## Service-Based Architecture
Similar to SOA (Service-Oriented Architecture).
Services are carved out without splitting the database.
Pros:
- Easier transition to microservices.
- Gains some agility benefits.

Cons:
- Risk of evolving into a “monolith of monoliths” if service boundaries aren't well-defined.
<!--stackedit_data:
eyJoaXN0b3J5IjpbNTc2MDg0NTg1LDIwNDU3NzU0NDJdfQ==
-->