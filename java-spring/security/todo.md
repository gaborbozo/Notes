* Filter
* Provider
* Authentication manager
* Authentication token
* Encoder
* User details service
* Security context
* Authentication interface

Firstly requests are go through filters. Security filters are ones which related to Spring security f.e UsernamePasswordAuthenticationFilter for processing credentials in a form

OAuth2/OIDC, LDAP, Custom, InDatabaseM - these and others are all supported by authentication provider

In a filter to know which is applied Spring defines Authentication manager which sits between filter and auth provider. In this obj there is Provider manager which looks for the match when authenticating.

In the end all authentication is the same. So Spring defiens UserDetailsService with the loadUserByUsername function to load the user from the user store (UserDetails object)

PasswordEncoder part of the Providers and its task is to encode the password before sending it to the user service

After successful auth Provider returns an Authentication object similar to the UserDetails

This Auth object is stored in SecurityContext. Another name for this is Principle. This context stored in the SecurityContextHolder

AWARE! This method only suits when we use a Session. Session is associated with the user. Cases when we not using a session, we have to reauth on every requests

Another example is Jwt auth - BearerTokenAuthenticationFilter - JwtAuthenticationProvider

Exception handling is managed by ExceptionTranslationFilter related to all the security

f.e filters: CsrFilter, DefaultLoginPageGeneratingFilter, DefaultLogoutPageGeneratingFilter, BasicAuthenticationFilter, AuthorizationFilter....

Multiple authentication filters can be used to authorize

yml:

logging:
 level:
   org.sprinframework.security: trace
<!--stackedit_data:
eyJoaXN0b3J5IjpbODA4MzkxODY2XX0=
-->