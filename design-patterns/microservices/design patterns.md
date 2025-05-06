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
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEzOTgzNjU4NzIsLTE4MDYwNTU5OTEsLT
M5OTgwODUxMSwtNTU4NDY2MDYzLDE5NzY5ODc0MDYsMTU0MzA4
Nzg0OV19
-->