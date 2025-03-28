`import java.lang.reflect.*;` runtime API

Allows to write a program that can "look at itself" and even "change itslef" while running based on information from a type descriptor (`.class`) file (JVM bytecode); classes, interfaces, annotations, enumeration types.
Arrays and primitives are not allowed.

Pros of reflection are
* Extensibility Features
* Class Browsers and Visual Development Environments
* Debuggers and Test Tools

Drawbacks
* Performance Overhead
* Security Restrictions
* Exposure of Internals

---
`.getClass` method returns the runtime class representation of the object which rpovides methods for accessing informations about a class.
## Modifiers
**Masking** - Each modifier corresponds to an int constant.
```java
class Method{
	public static final int ABSTRACT 1024
	public static final int FINAL 16
	public static final int INTERFACE 512
	public static final int NATIVE 256
	public static final int PRIVATE 2
	public static final int PROTECTED 4
	public static final int PUBLIC 1
	public static final int STATIC 8
	public static final int STRICT 2048
	public static final int SYNCHRONIZED 32
	public static final int TRANSIENT 128
	public static final int VOLATILE 64
}
```
`public int getModifiers()`
```java
public static void ... 
	-> getModifiers()
	// public + static
	-> 9 
```

## Informations
### Public
`getMethods(), getFields(), ...`
Inherited ones included
### All
`getDeclaredMethods(), getDeclaredFields()...`
`
Intherited ones excluded
### Filter
`getMethod(String, Class<?>...)`
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE2OTY3NTg1ODRdfQ==
-->