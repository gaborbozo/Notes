## DTO validation
`jakarta.validation`
1. `Size, Min, Max, NotNull, etc.` annotated on the dto's properties
2. On a function's argument add the `@Valid` keyword (`public void func(@Valid Type object)`)
## Globally handled exceptions
Instead of defining an `@ExceptionHandler` on a controller, a better practice may be to define a
```java
@ControllerAdvice
public class ExceptionHandler extends ResponseEntityExceptionHandler { ... }
```
in order to gain controll over the most general error cases. In this class handlers may be defined such as
```java

@ExceptionHandler(ResourceNotFoundException.class)
public final ResponseEntity<Object> handleResourceNotFoundException(
	ResourceNotFoundException ex, WebRequest request) {
	ProblemDetail pd = ProblemDetail.forStatusAndDetail(HttpStatus.NOT_FOUND, ex.getMessage());
	return createResponseEntity(pd, null, HttpStatus.NOT_FOUND, request);
}

@ExceptionHandler(Exception.class)
public final ResponseEntity<Object> handleGeneralException(Exception ex, WebRequest request) {
	ProblemDetail pd = ProblemDetail.forStatusAndDetail(HttpStatus.INTERNAL_SERVER_ERROR, ex.getMessage());
	return createResponseEntity(pd, null, HttpStatus.INTERNAL_SERVER_ERROR, request);
}
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTYxOTk1ODE5N119
-->