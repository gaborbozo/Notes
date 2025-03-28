# String

## String contstant pool
A reserved area within the heap. Multiple references can point to the same String pool value.
```java
// string1 & string2 point to the same address
String string1 = "text";
String string2 = "text";
// string3 does not, as it is not created in the String pool
String string3 = new String("text");
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbMzE0Mjg0MjJdfQ==
-->