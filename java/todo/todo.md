# Constant Pools
constant pool is a table of structures that contain symbolic references to classes, methods, fields, and other constants. 

It is a part of the Java class file format and is used by the Java Virtual Machine (JVM) during the execution of a Java program.
* **Storage of constants**: Stores various types of constants, such as numeric literals, string literals, class and interface names, field and method names, and other constant values.
* **Symbolic References:** Instead of directly embedding values in the bytecode, the constant pool uses symbolic references to represent these values. For example, instead of directly embedding the name of a method or a field in the bytecode, a symbolic reference to the method or field in the constant pool is used.
*  **Runtime Resolution:** During runtime, the symbolic references in the constant pool are resolved to actual memory addresses or values. This allows for flexibility and dynamic linking.
*  **Class Structure:** Each class file has its own constant pool, and it contains a combination of constant pool entries. The entries are indexed, and other parts of the class file refer to these indices to access the constants.
# Regex
```java
if (text.matches("[A-Za-z0-9]+@gmail.(com|hu)"))
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEzMTk5OTI3NzNdfQ==
-->