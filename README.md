# JSON Web Tokens (JWT)

## What is JWT?

A JSON Web Token, or JWT, is securely  sending data between two parties as JSON Object, usually a client and a server.


## When should you use JSON Web Tokens?

### Authentication
When a user logs in, the server can generate a JWT. The client can then store this token and send it with each subsequent request.

### Authorization
Once Signed Up, JWT can carry authorization information, such as user roles or permissions. By including this information in the token's payload, the server can determine what actions the user is allowed to perform.

### Information Exchange
JWTs can be used to securely exchange information between different parties.

## What is the JSON Web Token structure

It  consist of three parts separated by dots (.) which are:
 - header
 - payload
 - signature
 
**Ex:**

`eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpXVCIsImlhdCI6MTUxNjIzOTAyMn0.pNb0MEggBZd_JXFBuaqnXwmv_tdsUfWpQeTqOj5HQy4`

### Header

It describes how the token should be processed. It typically consist of  two parts: the token type, which is "JWT" in this case, and the algorithm used to secure the token.

**Example:**

```json
{
  "alg": "HS256",
  "typ": "JWT"
}
```

The header is Base64Url encoded to make first part of the JWT.


### Payload

The payload of a JWT contains the actual data or claims you want to transmit. Claims are statements about the user or any other information you want to include. There are three types of claims:
- registered claims
- public claims
- private claims

**Registered claims** are predefined by the JWT specification and include standard information like the issuer ("iss"), subject ("sub"), and expiration time ("exp"). 

**Public claims** are custom claims defined by you and can include any additional information relevant to your application. 

**Private claims** are custom claims agreed upon between parties and are not defined in the JWT specification.

**Example:**

```json
{
  "sub": "1234567890",
  "name": "JWT",
  "admin": true
}
```

The payload is Base64Url encoded  as the second part of the JWT.

### Signature

The signature is created by taking the encoded header, the encoded payload, a secret key known only to the server, and applying a cryptographic algorithm specified in the header. 

The signature ensures the integrity of the token and verifies that it hasn't been tampered with during transmission.

**Example**

HMACSHA256(
  base64UrlEncode(header) + "." +
  base64UrlEncode(payload),
  secret)
 

The signature is appended as the third part of the JWT.

## How JSON Web Tokens work?

![](https://firebasestorage.googleapis.com/v0/b/img-storage-2e6da.appspot.com/o/jwt-work-flow.png?alt=media&token=887f06fe-b2d8-404f-b79d-77985c78c8aa)

- The client sends credentials (e.g., username and password) to the Authentication Server.
- The Authentication Server verifies the credentials and authenticates the user.
- Upon successful authentication, the Authentication Server generates a JWT containing user information, such as the user's ID or roles.
- The JWT is sent back to the client.
- The client stores the JWT, typically in local storage or a cookie.
- For subsequent requests, the client includes the JWT in the "Authorization" header.
- The server receives the request and verifies the JWT's signature and integrity. It also decodes the JWT to access the user information.
- The server performs necessary operations based on the user information, such as authorizing the request, retrieving user-specific data, or applying appropriate access controls.

