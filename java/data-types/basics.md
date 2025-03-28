# Data types
**Variables, parameters, and references** are stored on the **stack** (execution stack) while **arrays, objects, and their members** are stored on the **heap**.
## Garbage Collector
Java's implementation for memory cleanup. Its essence is to "traverse" the heap, looking for objects that are no longer referenced.
# Primitives
Primitive types in Java are declared at compile time and are stored on the stack at runtime. When a primitive variable is declared, the compiler reserves a block of memory on the stack to hold its value

* `byte` - a signed 8-bit integer value that can range from $-128$ to $127$
* `short` - a signed 16-bit integer value that can range from $-32768$ to $32767$
* `int` - a signed 32-bit integer value that can range from $-2147483648$ to $2147483647$
* `long` - a signed $64$-bit integer value that can range from $-9223372036854775808$ to $9223372036854775807$
* `float` - a $32$-bit single-precision floating point value
* `double` - a $64$-bit double-precision floating point value
* `char` - a single $16$-bit Unicode character
* `boolean` - a value that can be either true or false

Primitive types are also inherently thread-safe, as each thread has its own stack with its own copies of the variables
## Casting
### Wideing
Implicit, automatically converts data
```java
int a = 3;
double b = a;
```
### Narrowing
Explicit, forcing it to convert into data, comes with losing data
```java
double pi = 3.14;
int a = (int)pi; //a=3
```
## Wrapper
Wrapper classes allows primitive data types to be used as objects by converting them into objects and vice versa
Every primitive has it's own wrapper class
These classes are immutables
### Autoboxing and unboxing
primitive to wrapper (autoboxing)
```java
List<Integer> list = new ArrayList();
for(int i =0;i < n;++i)
	//list.add(Integer.valueOf(i));
	list.add(i);
```
primitive from wrapper (autounboxing)
```java
void sum(List<Integer> list)
int sum = 0;
for(Integer item : list)
	//sum += item.intValue();
	sum += item;
```
Both called automatically by Java
# Immutable
Classes from which **neither inheritance nor modification of their values is allowed** are considered immutable and have the following properties:

-   An instance can be assigned values through a constructor.
-   No setters are present.
-   `final class`
-   Deep cloning for all mutable members (getter)
-   Deep cloning for the class (getter)
## Inner Value Leakage
Immutable data types have values that cannot be changed based on the reference.
```java
String string = "";
return string;

int a = 5;
return a;
...
```
But for mutable types, yes
```java
// Incorrect
int[] array = {1,2,3};
return array;

MutableObject object = new MutableObject();
return object;
// Correct
int[] array = {1,2,3};
return Arrays.copyOf(array,array.length);

MutableObject object = new MutableObject();
return new MutableObject(object);
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTExMDIyMTA3MDZdfQ==
-->