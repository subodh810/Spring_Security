Q. Your API should be accessible only by ADMIN users. How would you implement it?
>>To restrict an API to ADMIN users only, I would configure Spring Security using either URL-based authorization with hasRole("ADMIN") or method-level security using @PreAuthorize("hasRole('ADMIN')").

>>After JWT authentication, the user's roles are stored in the Authentication object inside SecurityContextHolder. When the request reaches the protected endpoint, Spring Security checks whether the authenticated user has the ROLE_ADMIN authority.

>>If the user has the ADMIN role, access is granted; otherwise Spring returns 403 Forbidden. If the user is not authenticated, Spring returns 401 Unauthorized.


Q. You need public APIs and secured APIs in the same application. How would you configure it?
>>To configure public and secured APIs in the same Spring Boot application, 

>I would use requestMatchers() in the SecurityFilterChain. Public endpoints such as /auth/login and /auth/register would be configured with permitAll(),

>while protected endpoints would use authenticated(). <br>
For role-based access, endpoints such as /admin/** would be secured using hasRole("ADMIN"). 

>In a JWT-based application, public APIs are accessible without a token, whereas secured APIs require a valid JWT that is validated by a custom JWT filter before authorization checks are performed.


Q. How do you secure Microservices using JWT?
>>To secure microservices using JWT, I would create a dedicated Authentication Service responsible for validating users and issuing JWT tokens.

>After login, the client receives a JWT and sends it with every request in the Authorization header. 

>An API Gateway validates the token before forwarding requests to downstream services. 

>Each microservice can also validate the JWT signature, expiration, and roles, then create an Authentication object and store it in SecurityContextHolder. 

>Authorization is enforced using roles or authorities such as hasRole('ADMIN'). Since JWT is stateless, no server-side sessions are required, making it highly scalable for microservice architectures.


Q. A JWT token expires after 15 minutes. How would you allow the user to continue without logging in again?
>>To avoid forcing the user to log in again when the JWT Access Token expires, I would implement a Refresh Token mechanism.

>During login, the server issues both a short-lived Access Token and a long-lived Refresh Token. 

>When the Access Token expires, the API returns 401 Unauthorized.

>The frontend interceptor catches this response and sends the Refresh Token to a dedicated refresh endpoint.

>After validating the Refresh Token, the backend generates a new Access Token and returns it to the client. The frontend then retries the original request with the new token.
If the Refresh Token is also expired, the user is redirected to log in again.


Q. A user has USER and ADMIN roles. How would Spring Security handle authorization?
>>If a user has both USER and ADMIN roles, Spring Security stores both authorities in the Authentication object inside SecurityContextHolder. During authorization, Spring checks whether the authenticated user possesses the required role. 

>For an endpoint protected with hasRole("ADMIN"), access is granted because the user has the ADMIN role. Similarly, access is granted to endpoints requiring USER role. If the endpoint requires a role that the user does not have, such as MANAGER, Spring returns 403 Forbidden. The authorization decision is based on the authorities present in the Authentication object.


Q. How would you implement logout in a stateless JWT application?
>>In a stateless JWT application, logout is usually implemented on the client side by removing the JWT token from storage (LocalStorage, SessionStorage, or cookies). Since the server does not maintain session state, simply deleting the token prevents future authenticated requests.

>However, if immediate token invalidation is required, the server can maintain a token blacklist or use short-lived access tokens with refresh tokens.


Q. How would you secure file upload APIs?
>>Securing file upload APIs is critical because uploaded files can contain malware, malicious scripts, oversized payloads, or unauthorized content.

>"To secure file upload APIs, I implement authentication and authorization, validate file type and size, scan files for malware, store files outside the web root, generate unique file names, and restrict access to uploaded files."


Q. How would you secure sensitive endpoints like /payment and /transfer?
>>Endpoints like /payment and /transfer are high-risk APIs because they involve financial transactions. Simply securing them with JWT authentication is not enough.

>"For sensitive endpoints such as /payment and /transfer, I would implement multiple security layers including strong authentication, fine-grained authorization, input validation, encryption, rate limiting, transaction verification, auditing, and fraud detection."


Q. A frontend Angular application is calling your Spring Boot APIs. What Spring Security configurations are required?
>>When an Angular frontend calls Spring Boot APIs, the main Spring Security configurations are:<br>
CORS configuration,
JWT/OAuth2 authentication,
CSRF configuration, 
Public and protected endpoint rules, 
Security Filter Chain setup &  
HTTPS enforcement (production)

>"When Angular calls Spring Boot APIs, I configure CORS for cross-origin requests, implement JWT-based stateless authentication, disable CSRF for JWT APIs, add a JWT filter in the Security Filter Chain, define public and protected endpoints using request matchers, enforce role-based authorization, and secure all communication through HTTPS in production."


Q. How would you prevent password theft even if the database is compromised?
>>To protect user passwords even if the database is breached, I would never store passwords in plain text. Instead, I would store them using a strong one-way hashing algorithm such as BCrypt or Argon2 with a unique salt for each password. This ensures that even if attackers gain access to the database, they only get hashed values, not the actual passwords."

>>"In Spring Boot, I typically use BCryptPasswordEncoder because it automatically generates a unique salt and is computationally expensive, making brute-force attacks difficult. For additional security, I would enforce strong password policies, enable Multi-Factor Authentication (MFA), implement account lockout or rate limiting after multiple failed login attempts, and monitor against known breached passwords.

>"I would also avoid using fast hashing algorithms like SHA-256 for password storage because they are vulnerable to GPU-based brute-force attacks. Password-specific algorithms such as BCrypt or Argon2 are designed to be slow and resistant to rainbow table attacks."
