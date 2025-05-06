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

Telemetry makes this pattern ef

1. Start with defining the domain not the database schema.
2. Evaluate actions that need to be performed.
3. 
## Business process-based microservices
<!--stackedit_data:
eyJoaXN0b3J5IjpbOTQxMjI0MDE4LC0zOTk4MDg1MTEsLTU1OD
Q2NjA2MywxOTc2OTg3NDA2LDE1NDMwODc4NDldfQ==
-->