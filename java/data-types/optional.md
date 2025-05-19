# Optional
Generic container object that may or may not contain a non-null value. Only used for returning values not for passing. This is because of serialization may not like it.

```java
Optional.empty();
Optional.of();
// defining default value
Optional.ofNullable();

// possile NoSuchElementException
optionalObj.get();
// default value if null
optionalObj.get().orElse();
// Similar to orElse(), but Supplier is specified instead of value
optionalObj.orElseGet();

// If the element doesn't match the Predicate, it reuturns Optional.empty()
optionalObj.filter();

// Specifies an operation to be applied to the non-null value; if there is no value, it will return an Empty Optional
optionalObj.map();
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTY1MTM5MDUxN119
-->