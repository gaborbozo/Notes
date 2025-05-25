# 1. Codebase; SCM and revision control
Must be tracked in a version control system.
Single application in a single repository.
> The strategy of managing the repository is up to the team.

Multiple environments handled through deploys.
```mermaid
graph LR
Non-Prod ---> Prod
Feature ---> Non-Prod
```
# 2. Managing dependencies
Dependencies are declared in a manifest which along with defining the dependencies, it defines their versions. Build system must package this manifest for the application to use during deployment and runtime.

Under no circumstances multiple applications would share a common dependency, each application should run in its own sandbox and execute as if there is nothing provided by the underlying operating system.

Because of this the application becomes truly portable, which is very imported in a distributed model. Other major benefit is easier onboarding for a new developer - because of the lack of complex setup.
# 3. Application configuration
Configuration includes all values needed by the application, but specific to the environment. Separate config from code to allow different deployments without changes to code.

Accomplished through
* external services,
* environmental varaibles,
* user-provided services.
# 4. Backing services
Backing service (like databases, queues) in a cloud native application include any service that is communicated with any service over any network. Each of the services is mounted to the application as a component. Access them via URLs or credentials, making them easy to swap or scale independently.

| Monolithic application workflow change | Twelve-factor application workflow change  |
|--|--|
| Modify code | Build db in production |
| Test in lower environment | Stop service and switch bindings |
| Build db in production and keep in sync | Start service |
| Deploy code |  |
| Hope it works |  |
# 5. Build, release, run; CI/CD
* Build creates a deployable package,
* release binds config to it,
* run executes the app.

There should be distinct phases of a lifecycle of a deployed application version.
# 6. Running processes
Applications themselves are deployed as one or more processes instead of embedding them into another process.

In cloud native system we are running processes that are stateless.  We should assume that there is no guarantee that data in memory will be there outside the runtime of the current process.
* single-threaded memory usage,
* short-lived memory usage.

Leverage databases or caches for longer-term memory needs.
# 7. Port binding
In twelve factor apps there is no separate container handling requests and reponses, instead the application needs to handle communication itself.

Export services via port binding.
# 8. Concurrency; Scaling with processes
Horizontal scaling of processes to achieve concurrency instead of vertical scaling.
# 9. Disposability
Important because of
* security - processes and applications have short lives in order to minimize the impact of an application instance being compromised,
* scalability - a process that start and shutsdown fast allows for an environment with auto scalable application instances,
* crashes happen.

Design aspects include
* **fast startup** - focus on things that are not immediately needed when a process starts up.
* **handling shutdowns appropriately (graceful shutdowns)**.
# 10. Dev/prod parity
Keeping development, staging, and production environments as similar as possible to reduce bugs and deployment friction.

Differences between environments often cause:
* Bugs that only appear in production,
* Configuration mismatches.
# 11. Logs
Logs are treated as an event data stream:
* each application writes its logs to standard out in the form of a stream,
* each applications share the same stream.

The logs can then be aggregated to another system. Do not manage log files; instead, stream logs to a centralized system.

Log routing technologies.
# 12. Administering
These tasks are treated as first class processes. They are themselves applications that are spawned when needed usually, by some overall management application. 

Run admin or one-off tasks in the same environment as regular app processes ensuring consistency and avoiding environment drift.
# 13. API first
Design and expose all functionalities through APIs before implementing UIs or clients.
1. contract is the promise that the code must adhere to,
2. build _API_,
3. consumption (Frontend, UI) is the last to implement. 

OpeanAPI specifications:
* define services,
* define objects,
* define errors: consider returning contextual data,
* check into _SCM_,
* consider publishing.

This ensures modularity, easy integration, and reusability across systems. APIs act as contracts that teams can work against independently.
# 14. Telemetry
Applications should emit logs, metrics, and traces for observability. This allows developers and operators to monitor health, detect issues, and analyze performance.

Cloud-native systems rely on external tools to collect and visualize this data. It supports continuous improvement and faster debugging.

* Logs tell what happened,
* metrics tell how and when they happened,
* tracing tell where it happened and who it happened to.
# 15. Authentication and authorization
Consider _AuthN_ and _AuthZ_ patterns early on the process. Use standardized protocols like OAuth2 or OpenID Connect.

Centralized identity management simplifies user control across services. It ensures compliance and secure operation in distributed cloud systems.
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTI2MzU3MjU1Nl19
-->