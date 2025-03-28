A class `B` depends on class `A` if `B` ceases to exist with the cessation of `A` (**tightly coupled**).

The fundamental problem is that the creation of class `B` happens with some "operation" inside `A` (function call, constructor, etc.). Furthermore, this raises the issue that we often unnecessarily allocate objects on the heap that we don't even use.

**DI** is an implementation of **Inversion of Control**. Its essence is that we "inject" `B` into `A` (**loosely coupled**). This task is performed by the IoC container, provided that the appropriate annotations are given or a pre-defined XML file is used. The classes created by the container are referred to as **Spring Beans**.

## Possible injections
### Setter-based
```java
@Autowired
public void setB(B b){
	this.b = b;
}
``` 
### Constructor-based
```java
@Autowired
public A(B b){
	this.b = b;
}
```
### Field-based
```java
@Autowired
B b;
```
## Microservices

Thanks to D.I, individual units become scalable. Furthermore, there's the possibility to dynamically modify the resources of these individual units.

## Bean Scopes

-   **singleton**: a single instance
-   **prototype**: a new instance every time
-   **request**: an instance per request
-   **session**: an instance per session
-   **globalSession**

`@Scope("singleton")`
<!--stackedit_data:
eyJoaXN0b3J5IjpbMzYxOTEyNTQwXX0=
-->