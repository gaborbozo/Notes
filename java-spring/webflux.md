# Traditional Spring MVC model
* Every HTTP request is handled by a dedicated thread,
* Logic is written in a blocking, imperative style,
* Uses _Servlet API_, typically backed by _Tomcat, Jetty,_ or _Undertow_.
1. A request comes into the _Servlet container_ (e.g., _Tomcat_).
2. A thread is taken from a pool (or created) to handle it.
3. The request is routed to a Controller method.
4. If the controller calls a database, _REST_ service, or file, the thread waits (blocks) for that _I/O_ to complete.
5. When everything is ready, the thread sends the response back.
6. The thread is released.

Limitations are:
* blocking threads (threads are expensive; can't scale well under load),
* thread starvation (under heavy load, all threads might be waiting for _I/O_, and now new requzest can be served),
* wasted resources (idling _CPU_)
# WebFlux
> **Event loop** is a programming construct that handles and dispatches events or messages in a non-blocking, asynchronous way.
> Instead of waiting for an operation to finish, **it registers a callback and moves on**.

**Web server** listens for incoming HTTP requests and sends back HTTP responses. Instead of _Tomcat or Jetty_, _WebFlux_ using _Netty_, which is **non-blocking and event-loop-based**.

**_Web API_** is the interface exposed by backend application via _HTTP_ - _REST_ endpoints, or _GraphQL APIs_.

**_WebFlux_** is a reactive web framework in the Spring ecosystem. Its key traits are
* Asynchronous & non-blocking,
* uses **_Project Reactor_** (Mono, Flux),
* and ideal for high-throughput, low-latency apps.
---
```
Request arrives
   ↓
[ Event Loop (Netty) ]
   ↓
[ Web Server (Netty embedded in Spring Boot) ]
   ↓
[ WebFlux (handles routing, reactive streams) ]
   ↓
[ Web API endpoint matched ]
   ↓
[ Controller method executed (returns Mono/Flux) ]
   ↓
[ Response streamed back to client ]
```
---
We define the logic using `Mono<T>` or `Flux<T>` (e.g., in a controller or service) — how data is fetched, created, combined.

_Spring WebFlux_ orchestrates the flow; subscribes to our reactive streams, connects lifecycle events, manages backpressure, etc.

_Netty_ sends and receives _HTTP_ traffic using non-blocking _I/O_. It doesn’t care if we use `Mono`, it just needs bytes eventually.

---
## Reactive publisher
Spring Reactive `Publisher` is an object that implements the Reactive Streams Publisher interface, and it emits data asynchronously and non-blockingly.
```java
public interface Publisher<T> {
    void subscribe(Subscriber<? super T> s);
}
```
Mono and Flux implement this interface. They don't do the work immediately — they describe how the work will be done when someone subscribes.

When a _Mono_ or _Flux_ returned from a controller, we are giving Spring a reactive publisher that it can subscribe to later, when it’s ready to send data to the client.
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTMzNTE1Mzc4MF19
-->