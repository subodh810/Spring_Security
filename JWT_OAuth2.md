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
