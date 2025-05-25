# SCM and revision control
Must be tracked in a version control system.
Single application in a single repository.
> The strategy of managing the repository is up to the team.

Multiple environments handled through deploys.
```mermaid
graph LR
Non-Prod ---> Prod
Feature ---> Non-Prod
```
# Managing dependencies
Dependencies are declared in a manifest which along with defining the dependencies, it defines their versions. Build system must package this manifest for the application to use during deployment and runtime.

Under no circumstances multiple applications would share a common dependency, each application should run in its own sandbox and execute as if there is nothing provided by the underlying operating system.

Because of this the application becomes truly portable, which is very imported in a distributed model. Other major benefit is easier onboarding for a new developer - because of the lack of complex setup.
# Application configuration
Configuration includes all values needed by the application, but specific to the environment.

Accomplished through
* external services,
* environmental varaibles,
* user-provided services.
# Backing services
Backing service in a cloud native application include any service that is communicated with any service over any network. Each of the services is mounted to the application as a component.

| Monolithic application workflow change | Twelve-factor application workflow change  |
|--|--|
| Modify code | Build db in production |
| Test in lower environment | Stop service and switch bindings |
| Build db in production and keep in sync | Start service |
| Deploy code |  |
| Hope it works |  |
# Build, release, run; CI/CD
-   compiling the app and dependencies
-   combining build with config
-   executing in an environment

There should be distinct phases of a lifecycle of a deployed application version.
# Running processes
Applications themselves are deployed as one or more processes instead of embedding them into another process.

In cloud native system we are running processes that are stateless.  We should assume that there is no guarantee that data in memory will be there outside the runtime of the current process.
* single-threaded memory usage,
* short-lived memory usage,

Leverage databases or caches for longer-term memory needs.
# Port binding
In twelve factor apps there is no separate container handling requests and reponses, instead the application needs to handle communication.
# Scaling with processes
Horizontal scaling of processes to achieve concurrency instead of vertical scaling.
# Disposability

<!--stackedit_data:
eyJoaXN0b3J5IjpbMTY1MDY4OTgyN119
-->