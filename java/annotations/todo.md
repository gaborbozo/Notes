# Annotations
```java
public @interface CustomAnnotation{}
```
### Checking for the presence
```java
@VeryImportant
class Dog{ }

...

if (dog.getClass().isAnnotationPresent(VeryImportant.class)
```
## Parameters
A parameter can only be `primitve`,  `class`, `string` or an `array`
```java
@Target(ElementType.METHOD)
public @interface RunImmediately{
	int times() default 1;
}
```
With reflection we can do things like this
```java
for (Method method : dog.getClass().getDeclaredMethods())
	if (method.isAnnotationPresent(RunImmediately.class){
		RunImmediately annotation = method.getAnnotation(RunImmediately);
		for (int i = 0;i < annotation.times(); i++)
			method.invoke(dog);
	}
}
```
In case of a field
```java
for (Field field : dog.getClass().getDeclaredFields()){
	if (field.isAnnotationPresent(ImportantField.class)){
		Object objectValue = field.get(dog);
		...
	}
}
```
## Attributes
### `Target` - `ElementType`
```java
@Target(ElementType.CLASS)
public @interface CustomAnnotationForClasses{}

// ElementType.METHOD/FIELD/TYPE/ANNOTATION/CONSTRUCTOR/PACKAGE/MODULE etc.

// multiple element types
@Target({ElementType.TYPE, ElementType.CLASS})
```
### `Retention` - `RetentionPolicy`
It determines how long the annotated elements and their associated annotations should be retained.
```java
@Retention(RetentionPolicy.RUNTIME)
public @interface CustomInterface{}

// Annotations are only retained in the source code and not included in the compiled bytecode or available at runtime.
RetentionPolicy.SOURCE,
// for example
@Override

// Annotations are to be recorded in the class file by the compiler but
// need not be retained by the VM at run time.
// Default
RetentionPolicy.CLASS,
// for example
@Deprecated

// Annotations are to be recorded in the class file by the compiler and 
// retained by the VM at run time, so they may be read reflectively.
RetentionPolicy.RUNTIME
// for example
@SuppressWarnings("unchecked")
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbNzMzNTk4ODg5XX0=
-->