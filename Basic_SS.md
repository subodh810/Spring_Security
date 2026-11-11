Q. Spring Security Architecture?
>>"Spring Security works through a filter-based architecture. Every request first passes through the Security Filter Chain, where authentication is performed using AuthenticationManager, AuthenticationProvider, and UserDetailsService. After successful authentication, user details are stored in SecurityContext, and authorization checks are applied based on roles and permissions before allowing access to application resources."


Q. How does Spring Security work internally?
>>"Internally Spring Security works using a filter-based architecture.<br> Every request first passes through the Security Filter Chain managed by FilterChainProxy.<br> During authentication, AuthenticationManager delegates to AuthenticationProvider, which uses UserDetailsService and PasswordEncoder to validate user credentials.<br> After successful authentication, an Authentication object is stored in SecurityContextHolder.<br> Then AuthorizationFilter checks whether the user has the required roles or authorities. If authorized, the request reaches the controller; otherwise Spring returns 401 or 403."


Q. What is the Security Filter Chain?
>>"Security Filter Chain is the core of Spring Security.<br> It is a collection of servlet filters that intercept every HTTP request before it reaches the controller.<br> The chain is managed by FilterChainProxy and contains filters responsible for authentication, authorization, exception handling, session management, and CSRF protection. When a request arrives, each filter executes in order. 

>For example, a JWT filter validates the token and stores the authenticated user in SecurityContextHolder. Then AuthorizationFilter checks roles and permissions. If all checks pass, the request reaches the controller; otherwise Spring returns 401 or 403."


Q. What are the default features provided by Spring Security?
>>"Spring Security provides several security features out of the box, including authentication, authorization, a default login page, CSRF protection, session management, logout handling, password encryption using BCrypt, security headers, exception handling, and a Security Filter Chain that intercepts every request.

>By default, all endpoints are secured and require authentication unless explicitly configured otherwise."


Q. What is UserDetailsService?
>>"UserDetailsService is a core Spring Security interface responsible for loading user information during authentication. It contains the loadUserByUsername() method, which retrieves user details such as username, password, roles, and authorities from a data source like a database. During login, AuthenticationProvider calls UserDetailsService, receives a UserDetails object, and then verifies the password using a PasswordEncoder. If the credentials are valid, Spring creates an authenticated user session."


Q. What is UserDetails?
>>UserDetails is a core Spring Security interface that represents an authenticated user. It contains security-related information such as username, password, roles, authorities, and account status. During authentication, UserDetailsService loads a UserDetails object, and Spring Security uses it to validate credentials and perform authorization checks.


Q. What is AuthenticationManager?
>>AuthenticationManager is the central Spring Security component that coordinates and delegates user authentication to appropriate AuthenticationProviders.


Q. What is AuthenticationProvider?
>>AuthenticationProvider is the Spring Security component that actually validates user credentials and creates an authenticated user object upon successful authentication.


Q. What is PasswordEncoder?
>>PasswordEncoder is a Spring Security component that hashes passwords before storage and validates passwords during authentication using secure one-way hashing algorithms such as BCrypt.


Q. Why is BCryptPasswordEncoder preferred?
>>BCryptPasswordEncoder is preferred because it automatically adds a unique salt to each password, stores passwords as secure hashes, and is intentionally slow to prevent brute-force attacks. This makes user passwords much safer than older algorithms like MD5 or SHA-1.


Q. What is the role of SecurityContextHolder?
>>SecurityContextHolder stores the currently authenticated user's Authentication object so that Spring Security can identify and authorize the user throughout the request lifecycle


Q. What is the Authentication object?
>>Authentication is the object that represents the currently logged-in user and their authorities in Spring Security


Q. Authentication and Authorization?
>>Authentication is the process of verifying the user's identity using credentials such as username and password.<br>
>When a request comes to a Spring Boot application, it first passes through the Spring Security Filter Chain.<br>
->For authentication, UsernamePasswordAuthenticationFilter extracts credentials and sends them to AuthenticationManager, which delegates to AuthenticationProvider.<br>
->The provider uses UserDetailsService to load user details from the database and validates the password.<br>
->If successful, the authenticated user is stored in SecurityContextHolder. After authentication, authorization begins.<br>
->Spring Security checks the user's roles and permissions through the AuthorizationFilter.<br>
->If the required role is present, the request reaches the controller;<br>
->otherwise, Spring returns a 403 Forbidden response.<br>

>Authentication answers "Who are you?" while authorization answers "What can you access?".


>>Authorization is the process of determining what an authenticated user can access.<br> 
->After successful authentication, Spring Security stores user details and roles in the SecurityContextHolder.<br>
->When a request arrives, the AuthorizationFilter checks the user's roles or authorities against the configured security rules.<br>
->If the required permission is present, access is granted and the request reaches the controller;<br>
->otherwise, Spring returns a 403 Forbidden response.
