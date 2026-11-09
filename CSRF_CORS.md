Q. CSRF?
>>CSRF, or Cross-Site Request Forgery, is an attack where a malicious website tricks an authenticated user into sending unwanted requests to another application where they are already logged in.

>The attack succeeds because browsers automatically send session cookies with requests. Spring Security protects against this by generating and validating CSRF tokens.

>CSRF protection should remain enabled for session-based applications, but it is commonly disabled for stateless JWT-based REST APIs because JWT tokens are sent explicitly in the Authorization header rather than automatically by the browser

Q. Why is CSRF protection enabled by default?
>>CSRF protection is enabled by default in Spring Security because most web applications traditionally use session-based authentication with cookies. Since browsers automatically send session cookies with requests, applications become vulnerable to CSRF attacks. Spring Security follows a secure-by-default approach and therefore enables CSRF protection automatically. In stateless JWT-based APIs, where authentication is passed explicitly in the Authorization header, CSRF protection is typically disabled because the browser does not automatically send JWT tokens.

Q. Why do we disable CSRF for REST APIs?
>>We disable CSRF protection for REST APIs because they are typically stateless and use JWT or OAuth2 tokens for authentication. CSRF attacks depend on browsers automatically sending session cookies, but JWT tokens are sent explicitly in the Authorization header by the client application. Since the browser does not automatically attach the JWT token, traditional CSRF attacks are generally not possible, so CSRF protection is usually disabled in JWT-based Spring Boot APIs.

Q. What is CORS?
>>CORS, or Cross-Origin Resource Sharing, is a browser security mechanism that allows a server to control which external origins can access its resources. It is required when a frontend application, such as Angular running on localhost:4200, calls a backend API running on a different origin, such as Spring Boot on localhost:8080. In Spring Boot, CORS is configured using CorsConfigurationSource, @CrossOrigin, and enabled in Spring Security through http.cors()

Q. Why does CORS occur?
>>CORS occurs because browsers enforce the Same-Origin Policy, which prevents a web application from accessing resources hosted on a different origin. An origin is defined by protocol, domain, and port. When an Angular application running on localhost:4200 calls a Spring Boot API on localhost:8080, the browser treats them as different origins and blocks the request unless the backend explicitly allows the origin through CORS configuration.

Q. How do you configure CORS in Spring Security?
>>CORS (Cross-Origin Resource Sharing) is required when the frontend and backend are hosted on different origins. 

>For example, an Angular application running on http://localhost:4200 calling Spring Boot APIs running on http://localhost:8080. In Spring Security, I configure CORS by defining a CorsConfigurationSource bean that specifies allowed origins, methods, and headers, and then enable CORS in the Security Filter Chain using http.cors(). This allows trusted frontend applications to access backend APIs securely."

Q. Difference between CSRF and CORS?
>>CSRF and CORS address different security concerns. 

>CSRF is an attack where a malicious website tricks an authenticated user into sending unauthorized requests, so Spring Security uses CSRF tokens to prevent it. 

>CORS, on the other hand, is a browser security mechanism that controls communication between different origins, such as an Angular frontend and a Spring Boot backend. 

>CSRF is primarily relevant for session-based applications and is often disabled for JWT-based APIs, 
whereas CORS is commonly required in modern frontend-backend architectures.
