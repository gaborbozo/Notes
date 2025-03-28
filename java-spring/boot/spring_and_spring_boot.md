| Spring   | Spring Boot |
|----------|----------|
| Primary feature is Dependency Injection | Primary feature is Autoconfiguration |
| Smaller tasks requires boilerplate code | Reduce boilerplate code
| Explicit definitions of dependencies in pom.xml | Starter concept in pom.xml internally angles the required dependencies
| Server needs to set up | Offers embedded servers such as Jetty & Tomcat, etc |

# Spring boot
#### `@SpringBootApplication` is a convenience annotation adds the followings
* `@Configuration`,tags the class as a source of bean definitions for the application context.
* `@EnableAutoConfiguration`, tells Spring Boot to start adding beans based on classpath settings, other beans, and various property settings.
* `@ComponentScan`, tells Spring to look for other components, configurations, and services.
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE3NTQxODI5NDFdfQ==
-->