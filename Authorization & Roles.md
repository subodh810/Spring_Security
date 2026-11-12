Q. Difference between Role and Authority?
>>A Role is a high-level user category such as ADMIN, MANAGER, or USER, whereas an Authority is a specific permission such as DELETE_USER or APPROVE_LOAN.

>In Spring Security, roles are typically collections of authorities. We check roles using hasRole() and authorities using hasAuthority(). Roles help manage groups of permissions, while authorities provide fine-grained access control. In enterprise applications, we usually use both together.

Q. What is hasRole()?
>>Use hasRole() when you want to check a user's role, such as ADMIN, USER, or MANAGER.

>It is commonly used with @PreAuthorize for method-level security. 

>Spring automatically prefixes the role with ROLE_, so hasRole('ADMIN') internally checks for ROLE_ADMIN. 

>If the user has the required role, access is granted; otherwise, Spring Security returns a 403 Forbidden response.

Q. What is hasAuthority()?
>>hasAuthority() is a Spring Security expression used to authorize access based on a specific permission or privilege. 

>Use hasAuthority() when you want to check a specific permission, such as READ_USER, WRITE_USER, or DELETE_USER.

>It is commonly used with @PreAuthorize to implement permission-based access control at the method level.

>The main difference is that hasRole() automatically adds the ROLE_ prefix, whereas hasAuthority() checks the exact authority name.

Q. What are Granted Authorities?
>>Granted Authorities are the permissions or privileges assigned to an authenticated user in Spring Security. 

>They are stored in the Authentication object and are used during authorization decisions. 

>Examples include permissions like READ_USER, DELETE_USER, or TRANSFER_MONEY. 

>Even roles such as ADMIN are internally stored as Granted Authorities with the prefix ROLE_, such as ROLE_ADMIN. 

>Spring Security uses these authorities when evaluating expressions like hasAuthority() and hasRole().


Q. How do you implement Role-Based Access Control (RBAC)?
>>Role-Based Access Control (RBAC) in Spring Security is implemented by assigning roles such as ADMIN, USER, and MANAGER to users. These roles are typically stored in database tables and loaded during authentication using a custom UserDetailsService. During the authentication process, the user's roles are converted into GrantedAuthority objects and stored in the SecurityContextHolder, which Spring Security uses for authorization decisions.

>At the URL level, we can secure APIs using requestMatchers().hasRole() or hasAnyRole() within the Security Filter Chain. For example, only ADMIN users can access /admin/** endpoints.

>For more fine-grained control, we secure the service layer using method-level security annotations such as @PreAuthorize, @PostAuthorize, or @Secured. To enable these annotations, we use @EnableMethodSecurity in the security configuration class.

>In enterprise applications, roles are often combined with authorities (permissions) to achieve fine-grained access control. This ensures that users are authorized not only based on who they are (Role) but also based on what actions they are allowed to perform (Authority).

Q. How do you restrict access to ADMIN users only?
>>In Spring Security, I can restrict access to ADMIN users at both the URL level and the method level. 

>At the URL level, I use hasRole('ADMIN') in the Security Filter Chain.

>At the service or controller level, I use method-level security annotations such as @PreAuthorize('hasRole('ADMIN')'). 

>Spring Security then checks whether the authenticated user has the ROLE_ADMIN authority before granting access.

Q. How can one user have multiple roles?
>>In Spring Security, a user can have multiple roles by establishing a many-to-many relationship between Users and Roles. During authentication, all assigned roles are loaded from the database, converted into GrantedAuthority objects, and stored in the SecurityContextHolder. Spring Security then checks these roles during authorization using methods like hasRole() or hasAnyRole().

Q. 
