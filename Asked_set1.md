Q. Spring Security Architecture?
>>"Spring Security works through a filter-based architecture. Every request first passes through the Security Filter Chain, where authentication is performed using AuthenticationManager, AuthenticationProvider, and UserDetailsService. After successful authentication, user details are stored in SecurityContext, and authorization checks are applied based on roles and permissions before allowing access to application resources."


Q. How does Spring Security work internally?
>>"Internally Spring Security works using a filter-based architecture.<br> Every request first passes through the Security Filter Chain managed by FilterChainProxy.<br> During authentication, AuthenticationManager delegates to AuthenticationProvider, which uses UserDetailsService and PasswordEncoder to validate user credentials.<br> After successful authentication, an Authentication object is stored in SecurityContextHolder.<br> Then AuthorizationFilter checks whether the user has the required roles or authorities. If authorized, the request reaches the controller; otherwise Spring returns 401 or 403."


Q. Authentication and Authorization?
>>Authentication is the process of verifying the user's identity using credentials such as username and password.
>>When a request comes to a Spring Boot application, it first passes through the Spring Security Filter Chain.<br>
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
