Q. JWT and Flow?
>>JWT (JSON Web Token) is a compact, secure way to transmit user information between a client and a server. It is commonly used for authentication and authorization in modern applications.

>>Structure of JWT :- A JWT consists of 3 parts separated by dots
>1. Header<br>
Contains token type and signing algorithm.
>2. Payload<br>
Contains user information (claims).
>3. Signature<br>
Used to verify that the token has not been tampered with.

>Flow
>1. User sends username and password to the server.
>2. Spring Security authenticates the credentials.
>3. Server generates a JWT token.
>4. Token is returned to the client.
>5. Client stores the token (usually in memory or secure storage).
>6. For every request, the client sends: Authorization: Bearer <JWT_TOKEN>
>7. Spring Security validates the token.
>8. If valid, the request is processed; otherwise, access is denied.


Q: Can JWT be modified by the client?
>> The payload can be decoded and viewed, but if anyone modifies it, the signature becomes invalid and Spring Security rejects the token.


Q. Why use OncePerRequestFilter in JWT Authentication?
>>In Spring Security, JWT validation is typically implemented inside a custom filter that extends OncePerRequestFilter.
>OncePerRequestFilter guarantees that the filter executes only once for a single HTTP request.<br>
Without it, a filter might run multiple times during :-
Request forwarding, 
Internal dispatching, 
Error dispatching &
Async processing.<br>
This can lead to repeated JWT validation and unnecessary overhead.


Q. What is the difference between JWT and Session Authentication?
>>Session Authentication is stateful, where the server creates and stores a session after login and the client sends a session ID with every request. JWT Authentication is stateless,<br> where the server generates a signed token containing user information and the client sends that token on every request.

>Session-based authentication requires server-side storage, while JWT does not, making JWT more suitable for REST APIs, microservices, and Angular/React applications.


Q. What is the difference between Access Token and Refresh Token?
>>Access Token is a short-lived token used to access protected APIs,<br> while Refresh Token is a long-lived token used to obtain a new Access Token when the current one expires.

> Access Tokens are sent with every request, whereas Refresh Tokens are only sent to the authentication server when a new Access Token is needed. This improves both security and user experience.

>When a user logs in, the server generates an Access Token and a Refresh Token. The frontend sends the Access Token with every API request. When the Access Token expires, the server returns 401 Unauthorized. The Angular HTTP Interceptor catches this response and sends the Refresh Token to a dedicated refresh endpoint. After validating the Refresh Token, the backend generates a new Access Token and returns it to the frontend. The interceptor then retries the original API request with the new Access Token. If the Refresh Token is also expired, the user must log in again.
