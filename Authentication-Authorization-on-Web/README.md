# Autentication and Authentication on the Web.

- Authentication: The process of verifying the identity of an individual.
- Authorization: The process of checking what the user is allowed to do.

As HTTP is a stateless protocol, every call to the server is a fresh call with no trace or state of previous calls.
So the only way to remember the states of the application is either by using sessions or tokens of the user so that there is no need for that user needs to log in again and again to access the application.

### Stateful vs Stateless Authentication
- Stateful: Server keeps track of the user's state (session, cookies)
- Stateless: Server does not keep track of the user's state (JWT)

### There are two ways to authenticate users.
1. Cookie or Session based approach
2. JSON Web Token (JWT) based approach

# Cookie or Session based approach
1. User sent authentication request using the username and password.
2. The server creates a new sessionID, stores that sessionID along with the user's info in sessions Database.
    - In Memory
    - In Cache (Redis)
    - In Database (MongoDB, PostgreSQL)
3. Server put the sessionID in cookies header and stores in the client's browser.
    -   ```http
            HTTP/2.0 200 OK
            Content-type: text/html
            Set-Cookie: sid=2moo8l4j4k1j3n4ko32v03mj054gv7rjh9bvd; Domain=example.com; Path=/; Expires=Wed, 13 Feb 2024 22:23:01 GMT;
        ```
4. Client (browser) includes that cookies in every subsequent request. 
    -   ```http
            GET /sample_page.html HTTP/2.0
            Host: www.example.org
            Cookie: sid=2moo8l4j4k1j3n4ko32v03mj054gv7rjh9bvd
        ```
5. when the server receives a request, extract the sessionID and Look in the Database of sessions.

### Cookies
- An HTTP cookie is a small piece of data that a server sends to a user's web browser. The browser may store the cookie and send it back to the same server with later requests. It remembers stateful information for the stateless HTTP protocol.
- Used for three purposes:
    - Session management: Logins, shopping carts, game scores, or anything else the server should remember
    - Personalization: User preferences, themes, and other settings
    - Tracking: Recording and analyzing user behavior
- Attributes:
    - `HttpOnly`: ensure that the client can't access the cookie, it only sent in http requests.
    - `Secure`: only sent in HTTPS requests.
    - `Expires`: the expiration time of the cookie.
    - `Domain`:  specifies which server can receive a cookie.
    - `Path`: the path of the cookie
        - `/`: Matches all the paths.
        - `/docs`: Matches all the paths that starts with `/docs` but not `/`;
    - `SameSite`: lets servers specify whether/when cookies are sent with cross-site requests, This provides some protection against cross-site request forgery attacks (CSRF).

# Json Web Token Based approach.

JSON web token (JWT), is an open standard that defines a compact and self-contained way for securely transmitting information between parties as a JSON object.

Because of its relatively small size, a JWT can be sent through a URL, through a POST parameter, or inside an HTTP header, and it is transmitted quickly. A JWT contains all the required information about an entity to avoid querying a database more than once. The recipient of a JWT also does not need to call a server to validate the token.

JWT eliminates the problem of DB lookup, the user info is stored in the session token itself. To secure the user's info part of the token is signed using a secret which is only known to the server.

### Flow
- The authentication request is sent from the user (username and password)
- The request reached server
    1. The server authenticates the user
    2. The server creates JWT session token using the user's info without making DB Call.
- This JWT token is sent to the user for future use (may be in the form of a cookie or form of response).
- The browser then incudes JWT Token within every subsequent request to the server. So when the browser receives the JWT token it uses the secret to validate the signed part and gets the user info.


### Benefits of JWTS
- #### Scalability
    - JWT, has higher scalability due to its statelessness.
- #### Maintainability
    - As There is no dedicated Database for sessions, There's no need to maintain anything. 

### Using JWTs
- Authentication: When a user successfully logs in using their credentials, an ID token is returned.
- Authorization: Once a user is successfully logged in, an application may request to access routes, services, or resources . To do so, in every request, it must pass an Access Token, which may be in the form of a JWT.
- Information exchange: JWTs are a good way of securely transmitting information between parties because they can be signed.

### JWT Structure.
- Header: contains metadata about the type of token and the cryptographic algorithms used to secure its contents.
    -  ```json
            {
                "alg": "HS256", // the hashing algorithm used
                "typ": "JWT" // the token type
            }
        ``` 
- payload (set of claims): contains verifiable security statements, such as the identity of the user and the permissions they are allowed.
    -   ```json
            {
                "sub": "1234567890",
                "name": "John Doe",
                "admin": true
            }
        ```
- signature: used to validate that the token is trustworthy and has not been tampered.
    -   ```js
            HACSHA256(
            base64UrlEncode(header) + "." +
            base64UrlEncode(payload),
            secret)
        ```
## resources
- [MDN-Cookies](https://developer.mozilla.org/en-US/docs/Web/HTTP/Cookies)
- [JWT vs Sessions](https://www.loginradius.com/blog/engineering/guest-post/jwt-vs-sessions/)
- [User Authentication JWT vs session](https://blogs.halodoc.io/user-authentication-jwt-vs-session/)
- [Difference between Session Cookies vs. JWT (JSON Web Tokens), for session management.](https://medium.com/@prashantramnyc/difference-between-session-cookies-vs-jwt-json-web-tokens-for-session-management-4be67d2f066e)
- [nodejs-authentication-guide](https://www.loginradius.com/blog/engineering/guest-post/nodejs-authentication-guide/)
