Q. What is @PreAuthorize?
>>@PreAuthorize is a Spring Security annotation used for method-level authorization. It evaluates a security expression before a method executes. We can use it to restrict access based on roles, authorities, or custom conditions such as hasRole('ADMIN') or hasAuthority('READ_PRIVILEGE'). If the user does not satisfy the condition, Spring Security returns a 403 Forbidden response. To use it, method security must be enabled using @EnableMethodSecurity.

Q. Difference between @PreAuthorize and @PostAuthorize?
>>@PreAuthorize and @PostAuthorize are method-level security annotations in Spring Security.

>@PreAuthorize performs authorization before a method executes and is commonly used for role- and permission-based access control.

>@PostAuthorize performs authorization after the method executes and is mainly used when access decisions depend on the returned object, using returnObject in the security expression.

>In most applications, @PreAuthorize is used more frequently because it prevents unauthorized users from executing business logic.


Q. What is @Secured?
>>@Secured is a Spring Security annotation used for method-level authorization based on roles. It checks whether the authenticated user has one of the specified roles before allowing method execution. 

>For example, @Secured('ROLE_ADMIN') restricts access to ADMIN users only. Unlike @PreAuthorize, it supports only role-based checks and does not support complex authorization expressions, which is why @PreAuthorize is generally preferred in modern Spring Boot applications.


Q. How do you enable method-level security?
>>Method-level security is enabled using @EnableMethodSecurity in the Spring Security configuration class. Once enabled, we can secure individual methods using annotations such as @PreAuthorize, @PostAuthorize, @Secured, and @RolesAllowed. Spring evaluates these annotations before or after method execution and returns a 403 Forbidden response if the authorization rules are not satisfied.


Q. @PreAuthorize("hasRole('ADMIN')")? 
>>@PreAuthorize(\"hasRole('ADMIN')\") is a method-level security annotation that allows a method to execute only if the authenticated user has the ADMIN role. Spring Security evaluates this condition before invoking the method, and if the user does not have the required role, it returns a 403 Forbidden response


Q. How do you secure service-layer methods? 
>>I secure service-layer methods using Spring Security's method-level security annotations such as @PreAuthorize, @PostAuthorize, and @Secured. While URL-level security protects endpoints, service-layer security ensures that business logic remains protected even if the same service method is called from another controller, scheduler, or microservice.
