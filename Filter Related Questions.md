Q. What is a Servlet Filter?
>>A Servlet Filter is a server-side component that intercepts HTTP requests and responses before they reach the controller and after the response is generated. 

>It is typically used for cross-cutting concerns such as authentication, authorization, JWT validation, logging, CORS handling, and request auditing. 

>In Spring Security, the entire security framework is implemented using a chain of servlet filters, and custom JWT authentication is commonly implemented using a filter that extends OncePerRequestFilter.

Q. What is Spring Security Filter Chain?
>>The Spring Security Filter Chain is a sequence of security filters that intercept every incoming HTTP request before it reaches the controller. Each filter performs a specific security-related task such as authentication, authorization, session management, exception handling, CSRF protection, or JWT validation. The request passes through these filters one by one, and only if all security checks are successful does it reach the controller.

Q. Difference between Filter and Interceptor?
>>

Q. How do you add a custom filter?
>>In Spring Security, I add a custom filter when I need to implement custom request processing logic such as JWT authentication, API key validation, request logging, audit tracking, multitenancy, or custom authorization.

>The recommended approach is to create a filter by extending OncePerRequestFilter, implement the custom logic inside doFilterInternal(), and then register the filter in the Spring Security Filter Chain using addFilterBefore(), addFilterAfter(), or addFilterAt(). 

>For JWT-based applications, the filter is typically added before UsernamePasswordAuthenticationFilter so that token validation happens before authorization

Q. What is the execution order of filters?
>>"Spring Security processes every incoming HTTP request through a Security Filter Chain, which is an ordered collection of servlet filters. Each filter has a specific responsibility such as authentication, authorization, exception handling, session management, CSRF protection, or JWT validation. The request flows through these filters sequentially before reaching the controller. If any filter fails validation, the request is stopped and an appropriate response such as 401 Unauthorized or 403 Forbidden is returned.
