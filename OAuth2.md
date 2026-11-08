Q. What is OAuth2?
>>OAuth 2.0 is an authorization framework that allows third-party applications to access a user's resources without sharing their password.<br>
It works by authenticating the user through an Authorization Server, such as Google and issuing an Access Token to the client application. <br>The client then uses that token to access protected resources from a Resource Server.

>OAuth2 is widely used for social logins, API security, and Single Sign-On (SSO).


Q. Difference between OAuth2 and JWT?
>>OAuth2 and JWT solve different problems. 

>OAuth2 is an authorization framework that defines how a client obtains access to protected resources. 

>JWT is a token format used to securely store user information and claims. 

>In simple terms, OAuth2 defines the process of obtaining access, while JWT is often the token that carries that access information.

>A common example is "Login with Google," where OAuth2 manages the authorization flow and Google issues a JWT token to the application.


Q. How does Google Login work in Spring Security?
>>Google Login in Spring Security is implemented using OAuth2.

>When the user clicks "Login with Google", Spring Security redirects the user to Google's authorization server.<br> Google authenticates the user and asks for consent.<br> After approval, Google sends an Authorization Code back to the application.<br> Spring Security exchanges this code for an Access Token and retrieves the user's profile information from Google.<br> It then creates an authenticated OAuth2User object, stores it in SecurityContextHolder, and grants access to the application.<br> In modern applications, a JWT is often generated after successful Google authentication and returned to the frontend.


Q. Explain OAuth2 Authorization Code Flow.
>>OAuth2 Authorization Code Flow is the most commonly used OAuth2 flow.
>
>->When the user clicks Login with Google, the application redirects the user to Google's authorization server.<br>
->After successful login and user consent, Google sends an Authorization Code back to the application.<br>
->The backend then exchanges this code for an Access Token and optionally a Refresh Token.<br>
->Using the Access Token, the application retrieves user details and authenticates the user.<br>
->This flow is secure because the user's credentials remain with Google and the token exchange happens server-to-server.
