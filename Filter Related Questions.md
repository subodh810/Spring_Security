Q. What is a Servlet Filter?
>>A Servlet Filter is a server-side component that intercepts HTTP requests and responses before they reach the controller and after the response is generated. 

>It is typically used for cross-cutting concerns such as authentication, authorization, JWT validation, logging, CORS handling, and request auditing. 

>In Spring Security, the entire security framework is implemented using a chain of servlet filters, and custom JWT authentication is commonly implemented using a filter that extends OncePerRequestFilter.

Q. What is Spring Security Filter Chain?
>>"Security Filter Chain is the core of Spring Security.<br> It is a collection of servlet filters that intercept every HTTP request before it reaches the controller.<br> The chain is managed by FilterChainProxy and contains filters responsible for authentication, authorization, exception handling, session management, and CSRF protection. When a request arrives, each filter executes in order. 

>For example, a JWT filter validates the token and stores the authenticated user in SecurityContextHolder. Then AuthorizationFilter checks roles and permissions. If all checks pass, the request reaches the controller; otherwise Spring returns 401 or 403."


Q. Difference between Filter and Interceptor?
>>

Q. How do you add a custom filter?
>>In Spring Security, I add a custom filter when I need to implement custom request processing logic such as JWT authentication, API key validation, request logging, audit tracking, multitenancy, or custom authorization.

>The recommended approach is to create a filter by extending OncePerRequestFilter, implement the custom logic inside doFilterInternal(), and then register the filter in the Spring Security Filter Chain using addFilterBefore(), addFilterAfter(), or addFilterAt(). 

>For JWT-based applications, the filter is typically added before UsernamePasswordAuthenticationFilter so that token validation happens before authorization

Q. What is the execution order of filters?
>>A custom filter in Spring Boot is created by implementing the Servlet Filter interface or extending OncePerRequestFilter.

>>Filters intercept requests before they reach the Spring MVC controller and responses before they are returned to the client. 

>>Common use cases include JWT authentication, logging, auditing, request/response modification, CORS handling, and rate limiting. 

>>Filters can be registered using @Component, FilterRegistrationBean, or added to the Spring Security filter chain using addFilterBefore() and addFilterAfter().

>>The chain.doFilter() method must be called to pass the request to the next filter or controller. In Spring Security applications, OncePerRequestFilter is generally preferred for custom authentication filters.
