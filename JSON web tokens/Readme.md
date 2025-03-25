# JSON web tokens
### What are JWTs?
JSON web tokens (JWTs) are a standardized format for sending cryptographically signed JSON data between systems. They can theoretically contain any kind of data, but are most commonly used to send information ("claims") about users as part of authentication, session handling, and access control mechanisms.

Unlike with classic session tokens, all of the data that a server needs is stored client-side within the JWT itself. This makes JWTs a popular choice for highly distributed websites where users need to interact seamlessly with multiple back-end servers.

### JWT Format
A JWT consists of 3 parts: a header, a payload, and a signature. These are each separated by a dot, as shown in the following example:

 ```eyJraWQiOiI5MTM2ZGRiMy1jYjBhLTRhMTktYTA3ZS1lYWRmNWE0NGM4YjUiLCJhbGciOiJSUzI1NiJ9.eyJpc3MiOiJwb3J0c3dpZ2dlciIsImV4cCI6MTY0ODAzNzE2NCwibmFtZSI6IkNhcmxvcyBNb250b3lhIiwic3ViIjoiY2FybG9zIiwicm9sZSI6ImJsb2dfYXV0aG9yIiwiZW1haWwiOiJjYXJsb3NAY2FybG9zLW1vbnRveWEubmV0IiwiaWF0IjoxNTE2MjM5MDIyfQ.SYZBPIBg2CRjXAJ8vCER0LA_ENjII1JakvNQoP-Hw6GG1zfl4JyngsZReIfqRvIAEi5L4HV0q7_9qGhQZvy9ZdxEJbwTxRs_6Lb-fZTDpW6lKYNdMyjw45_alSCZ1fypsMWz_2mTpQzil0lOtps5Ei_z7mM7M8gCwe_AGpI53JxduQOaB5HkT5gVrv9cKu9CsW5MS6ZbqYXpGyOG5ehoxqm8DL5tFYaW3lB50ELxi0KsuTKEbD0t5BCl0aCR2MBJWAbN-xeLwEenaqBiwPVvKixYleeDQiBEIylFdNNIMviKRgXiYuAvMziVPbwSgkZVHeEdF5MQP1Oe2Spac-6IfA```

Using [JWT.io](https://jwt.io/)

The header and payload parts of a JWT are just base64url-encoded JSON objects. The header contains metadata about the token itself, while the payload contains the actual "claims" about the user.

Example decoded payload:

```json
{
    "iss": "portswigger",
    "exp": 1648037164,
    "name": "Carlos Montoya",
    "sub": "carlos",
    "role": "blog_author",
    "email": "carlos@carlos-montoya.net",
    "iat": 1516239022
}
```
## JWT Signature

The server that issues the token typically generates the signature by hashing the header and payload. In some cases, they also encrypt the resulting hash. This mechanism provides a way for servers to verify that none of the data within the token has been tampered with since it was issued:

- Changing any part of the header or payload invalidates the signature
- Without the secret signing key, it's impossible to generate a valid signature

## JWT vs JWS vs JWE

The JWT specification is actually very limited. It only defines a format for representing information ("claims") as a JSON object that can be transferred between two parties.

- **JWS (JSON Web Signature)**: The most common implementation, where the token contents are signed but not encrypted
- **JWE (JSON Web Encryption)**: Similar to JWS but with encrypted contents

> **Note**: Throughout these materials, "JWT" refers primarily to JWS tokens, although some vulnerabilities may also apply to JWE tokens.

## JWT Attacks

### What are JWT attacks?
JWT attacks involve a user sending modified JWTs to the server in order to achieve a malicious goal, typically to bypass authentication and access controls by impersonating another user.

### Impact of JWT Attacks
The impact is usually severe. If an attacker can create valid tokens with arbitrary values, they may:

- Escalate privileges
- Impersonate other users
- Take full control of accounts
- Bypass security controls

### How vulnerabilities arise
JWT vulnerabilities typically arise due to:

1. Flawed JWT handling within the application
2. Flexibility in JWT specifications leading to implementation mistakes
3. Failure to properly verify signatures
4. Weak secret keys that can be guessed or brute-forced
5. Leaked secret keys

These flaws often allow attackers to tamper with token payloads or generate valid tokens without knowing the proper secret key.



