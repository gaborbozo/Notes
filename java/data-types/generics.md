# Generics
Provides a way to create classes, interfaces, and methods that can work with different data types

They provide compile-time type safety meaning that if an error occurs it is related to incompatible data types (before code is even executed)

They are implemented by using type parameters
```java
public class GenericData<T>
```

The actual type is determined when an instance of GenericsData is created
```java
GenericData<Integer> data = new GenericData<Integer>();
```
### Raw type
A template type (for compatibility reasons) can be used without its parameters.
```java
public class Box<T> {
    public void set(T t) { /* ... */ }
    // ...
}
// To create a parameterized type of Box<T>
// need to supply an actual type argument for the formal type parameter T
Box<Integer> intBox = new Box<>();
// If the actual type argument is omitted, it is a raw type of Box<T>
Box rawBox = new Box();

// Non-generic class or interface type is not a raw type
```
**Raw types show up in legacy code** because lots of API classes (such as the Collections classes) were not generic prior to JDK 5.0.

For backward compatibility, assigning a parameterized type to its raw type is allowed
```java
Box<String> stringBox = new Box<>();
Box rawBox = stringBox;				// OK

// Assigning a raw type to a parameterized type leads to warning
Box rawBox = new Box();				// rawBox is a raw type of Box<T>
Box<Integer> intBox = rawBox;		// warning: unchecked conversion

// Warning if a raw type is used to invoke generic methods defined in the corresponding generic type
Box<String> stringBox = new Box<>();
Box rawBox = stringBox;
rawBox.set(8);						// warning: unchecked invocation to set(T)


// works, but deprecated
Map nameToBook = new HashMap();
// also works, but deprecated
Map nameToBook = new HashMap<String, Book>();
// the long form, supported by Java 5 and Java 6
Map<String, Book> nameToBook = new HashMap<String, Book>();
// this is the recommended way
Map<String, Book> nameToBook = new HashMap<>();
```
### Type erasure
## Bounded type parameters
Specifies a bound on the types that can be used as arguments for a type parameter allowing to restrict the types that can be used with the generic type.

**Upper-bound**`(? extends Field)` means argument can be any `Field` or **subclass** of `Field`.

**Lower-bound**`(? super Field)` means argument can be any `Field` or **superclass** of `Field`.
### Wildcard
`?` indicates the type parameter can be anything
```java
// Anything
void print(List<?> list)

// Anything which extends from the Animal class
void print(List<? extends Animal>)
```
### Multiple bounds
```java
// Convention is to only have one class (because Java does not support multiple inheritance)
// and class needs to be first 
class Printer <T extends Animal & Serializable>
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEzNjQ5MTM2NTZdfQ==
-->