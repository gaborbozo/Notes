# Try-with-resources
```java
//try-finally
BufferedReader in = ...;
try{
	//read
} finally{
	in.close();
}
//try-with-resources
try(BufferedReader in = ...;BufferedReader in2 = ...){
	//read
}
```
Ha a `BufferedReader` létrejön, akkor be is zárja azt implicit
# Ternary operator
```java
feltetel ? akkor : kulonben;
valtozo = feltetel ? akkor : kulonben;
```
# Array of var args
The two are equivalent
```java
String[] args;
String... args;
```
# Chaining
```java
public void multiplyWith(double value){
	this.value *= value;
}
//object.multiplyWith(#)
//object.multiplyWith(#)

//Chaining
public Object multiplyWith(double value){
	this.value *= value;
	return this;
}
//object.multiplyWith(#).multiplyWith(#);

```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTQ0MjgwMTc4OV19
-->