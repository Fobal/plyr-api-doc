---
description: Verify a session JWT locally
---

# Verify JWT Locally

{% hint style="info" %} Verify a session JWT locally using the ES256 algorithm and a public key. {% endhint %}

## Verification Process

To verify a JWT locally, you'll need:

1. The JWT token to verify
2. The public key in PEM format (base64 encoded)

### Parameters

```typescript
{
  token: string,      // The JWT to verify
  publicKey: string   // Base64 encoded public key (must be decoded to UTF-8 before use)
}
```

### Example Usage

```typescript
try {
    const decodedToken = jwt.verify(token, Buffer.from(base64PublicKey, 'base64').toString('utf-8'), { algorithms: ['ES256'] });
    // JWT is valid, decodedToken contains the payload
} catch (error) {
    // JWT verification failed
    console.error(error.message);
}
```

### Success Response

If verification succeeds, you'll get the decoded JWT payload:

```typescript
{
  plyrId: string,
  walletAddress: string,
  exp: number,
  // ... other claims from the JWT
}
```

### Error Cases

Verification will throw an error if:

-   The JWT format is invalid
-   The signature is invalid
-   The token has expired
-   The algorithm doesn't match (must be ES256)
