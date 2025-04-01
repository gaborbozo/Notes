Every type is either a reference or a primitive.
For every type of object, the Java virtual machine instantiates an immutable instance of `java.lang.Class` which provides methods to examine the runtime properties of the object including its members and type information.

If an instance of an object is available, then the simplest way to get its `Class` is to invoke `Object.getClass()`. 
```java
//Class of String
Class c = "foo".getClass();
```
## Retrieving class objects
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE1MDc2ODU3MDldfQ==
-->