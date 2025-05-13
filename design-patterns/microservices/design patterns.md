# Key terminologies
**Data service** connects to internal data sources (not just databases) and is usually domain-specific.
**Business service** is a higher-level abstraction built on data services, aligning with broader business domains.
**Translation service** wraps third-party services with your own interface.
**Edge service** interfaces directly with users or external systems (e.g., web or mobile clients).
# Decomposition patterns
Decomposing a problem into smaller blocks of work.
## Domain-based microservices
Lowest level of decomposition that might be seen in a microservices architecture. Goal is to make services more scalable.
> One of the most efficient way to make services smaller, and more focused.

Focuses on serving the data as it will be used throughout the system and applying logic within the domain itself.

It's possible that a domain shares enough functionality with anoter domain that it may trigger to merge them into a new single domain. The key is on **focusing the data and how it is actually used throughout the system**.

**Telemetry** (system data/metrics) helps refine domain boundaries more effectively than just relying on experience.

1. Start with defining the domain not the database schema.
2. Evaluate actions that need to be performed (not just CRUD).
3. After everything start to address the data store and underlying implementation details.
## Business process-based microservices
Business process-based microservices address complex workflows that span multiple domains (keeping the DRY principle). Unlike domain-based microservices, which focus on a single data domain, these services represent higher-level abstractions centered around business logic and processes.

**These services do not own or manage data directly** instead, they coordinate between domain services, maintaining a clear separation between business logic and data access. The goal is not to add unnecessary layers, but to provide meaningful abstraction - only where processes genuinely require cross-domain coordination.
## Atomic transaction-based microservices
Cases where atomic transactions a must have because eventual consistency is not good enough (atomic transactions that span multiple data domains).
> In the context of a single domain, there is no need to specialize a service, because the underlying implementation is hidden.

Providing cross-domain services that support failure domains and rollbacks of the entire domain **must force a blocking API call until the commit is succesful**.
> While logically can do these asynchronously, usually the caller needs a guarantee of success or an error, so the API must be synchronous and blocking.

Following this approach all tables need to be under the same database in order to force atomicity.
###  Distributed Transaction Protocol
Keeping tables in different databases with two phase commiting guarantees atomicity. 
## Strangler pattern (decomposing a legacy monolith application)
Gradual strategy for decomposing a monolithic system into microservices. It's idea is to strangle the monolith by creating microservices based on business processes, which can be achieved in two ways:
### Top-down (API first)
- Begin with building APIs and associated services,
- later, migrate the underyling data if needed.
### Bottom-up (Data first)
- Identify the domains within the monolith,
- move each domains to its own separate database and create corresponding services,
- redirect clients to the new services and remove legacy dependencies once migration is complete.
## Sidecar pattern (decomposing duplicated functions)
Offload common functionality [logging, monitoring, or security] into a separate, co-deployed module (separate standalone process) alongside each microservice, reducing code duplication and improving maintainability.
# Integration patterns
Orchestration and ingress needs across the system as a whole.
## Gateway pattern
It is an **ingress pattern** for client communicating with services. Designed to provide a buffer between the underlying services and the client needs. Can be accomplished via facade or simple proxy.

It offers **centrallized control over requests** (especially as client diversity grows [e.g, mobile, desktop, third-party vendors]), mutating, decorating, aggregating, or restricting calls based on client needs. Enables **consistent payload shaping** (do not need to bother on the service side when something have been changed), security, and scalability, while shielding internal services from direct exposure.

This pattern **must avoid business logic and maintain contract stability through strict versioning** (changes should only extend functionality (e.g., adding optional fields), never remove or change existing behavior) **and passive API behavior** (like `/v1/`, `/v2` ensuring older versions continue to work even if newer versions are released).
## Process aggregator pattern
It is an **orchestration pattern** used to combine multiple business processes into a single API call for clients - different business processes must be executed together, and their results combined into a unified response.

This patterns should contain business logic that governs how processes are invoked and how their results are merged, preventing clients from duplicating logic (keeping DRY) and ensuring consistent behavior across the system.

It is possible aggregators can become a **choke point** in the system if they involve sequential, long running operations (in such cases use asynchronous patterns [e.g., message queue, saga pattern, polling + webhooks or notifications, ..]).
## Edge pattern
It is an **ingress pattern** which purpose is to introduce dedicated edge services for each client type. 
> Though gateways simplify centralized maintenance, edge services offer greater agility and isolation, especially useful in mobile or high-variation client environments.

These service provide aggregation, consolidation, and complexity isolation tailored to the client, also more efficient scaling, since services scale based only on the clien's load. Supports better flexibility for adding new clients or updating APIs without impacting others and improved security, throught tighter control and isolation (e.g., with OAuth).
# Data patterns

## Single-service single-database
> In a microservices architecture, the service scalability needs should be proportional to the database's scaling needs.

> As load on a single service increases, the associated use of the database will also increase. This can cause you to size the database based on single-service peak needs when the entire system is underutilized.

**Each data domain get its own dedicated data store**. Caveat here is that if the domain also is included in an atomic transaction, we have to be a little bit less fine grained.

**As the service scales, the data store itself also scales** and since both the data domain and data store are isolated, they can be both scaled up without impacting the system as a whole.
## Shared service database


<!--stackedit_data:
eyJoaXN0b3J5IjpbMjA1Njc1Nzg3OSwyMDUwMTkxOTk1LDI1MT
YzOTYyNCwtMzY4Mjc5NTg4LC0xNDI3MTI1ODUyLDk2ODYyNzI0
MiwtMjA2NTQwNDkxMCw1Njg5MzQ3MTYsNDc1NTQ2MjI3LDIxMT
E0NTc0MjAsMTA5NDQ0OTIsMzQ0NjY0NDIyLDIwNDk3NDI2NzEs
LTEzOTgzNjU4NzIsLTE4MDYwNTU5OTEsLTM5OTgwODUxMSwtNT
U4NDY2MDYzLDE5NzY5ODc0MDYsMTU0MzA4Nzg0OV19
-->