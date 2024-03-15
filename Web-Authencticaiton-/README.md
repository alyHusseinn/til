# Json Web Token
JSON web token (JWT), is an open standard that defines a compact and self-contained way for securely transmitting information between parties as a JSON object.

Because of its relatively small size, a JWT can be sent through a URL, through a POST parameter, or inside an HTTP header, and it is transmitted quickly. A JWT contains all the required information about an entity to avoid querying a database more than once. The recipient of a JWT also does not need to call a server to validate the token.

### Benefits of JWTS
- More compact: JSON is less verbose than XML, so when it is encoded, a JWT is smaller than a SAML token.
- More secure: JWTs can use a public/private key pair in the form of an X.509 certificate for signing.
- Easier to process: JWT is used at internet scale. This means that it is easier to process on users' devices, especially mobile.

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