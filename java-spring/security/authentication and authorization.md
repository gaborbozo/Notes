# Authentication(AuthN) and Authorization(AuthZ)
Authentication is the process of determining who that a principal is who they say they are. Authorization (access control) determines what the principal can and cannot do.

Authentication can be handled through:
* _HTTP basic_,
* _HTTP digest_,
* _X.509_ certificate-based,
* Form-based.

## [#](https://github.com/spring-projects/spring-security/tree/main/core/src/main/java/org/springframework/security/core/userdetails)Authenticate

Spring security requires a `UserDetailService` implementation in order to authenticate users.

```java 
// Core interface which loads user-specific data.
interface UserDetailsService

// Extension which provides the ability to create new users and update existing ones.
interface UserDetailsManager extends UserDetailsService

// Provides core user information.
class UserDetails extends Serializable

// API for changing a UserDetails password.
interface UserDetailsPasswordService
```

```java
class InMemoryUserDetailsManager implements UserDetailsManager, UserDetailsPasswordService
```
## [#](https://github.com/spring-projects/spring-security/tree/main/crypto/src/main/java/org/springframework/security/crypto)Password hashing
```java
// Service interface for encoding passwords.
interface PasswordEncoder 
```

`BCryptPasswordEncoder` is the default `PasswordEncoder` implementation if not defined.
## Authorities
```java
import java.security.Principal;

// Represents an entity, such as an individual user, a group, or a corporation,
// that can be authenticated and identified in a security context.
interface Principal

// Represents the token for an authentication request or for an authenticated principal.
// Once the request has been authenticated, the Authentication will usually be stored in a
// thread-local SecurityContext managed by the SecurityContextHolder.
interface Authentication extends Principal, Serializable

// Base class for Authentication objects.
// CredentialsContainer - indicates that the implementing object contains sensitive data, which can be erased
abstract class AbstractAuthenticationToken implements Authentication, CredentialsContainer

// An Authentication implementation that is designed for simple presentation of a username and password.
class UsernamePasswordAuthenticationToken extends AbstractAuthenticationToken
```
# LDAP (Lightweight Directory Access Protocol)
* Built into many operating systems,
* ineroperable,
* highly scalable.

`spring-security-ldap` project full support for native _LDAP_ operations.

It leverages the `AuthenticationManagerBuilder` in the same manner.
# OAuth2
Protocol and framework for providing access to _HTTP_ services.
> Often used for third-party access.

Can be used for system-to-system communications in standalone mode or on behalf of a user.

**Resource** owner is often the user, the data being protected.
**Client** is the application requesting access,
**Resource server** hosts protected data and accounts,
**Authorization server** is the service that grants tokens.

**Access token** is a secret and ofthen short-lived token that identifies a user.
**Refresh token** is a longer-lived token used to renew the access token when it expires.
**Scopes** provide for rights associated with the access token (read, write, etc.).

**Authorization code grant** is most common.
**Implicit grant** is common in web apps and mobile apps.
**Client credentials grant** is useful in system-to-system communications. Each system gets a client ID and a secret that is uses to get an access token and then do its work within the system based on the scopes.
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTYxNTgzNTAxMV19
-->