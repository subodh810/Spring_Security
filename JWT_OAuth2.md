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
