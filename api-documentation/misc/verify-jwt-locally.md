---
description: Verify a session JWT locally
---

# Verify JWT Locally

{% hint style="info" %} Verify a session JWT using the local public key. {% endhint %}

**Endpoint:** `/auth/verify`  
**Method:** POST

{% tabs %} {% tab title="Request Body" %}

```typescript
{
  sessionJwt: string,  // JWT to verify
  publicKey: string   // Public key in PEM format
}
```

{% endtab %}

{% tab title="Success Response (200)" %}

```typescript
{
  success: true,
  data: {
    isValid: boolean,
    payload?: {
      plyrId: string,
      walletAddress: string,
      exp: number
    }
  }
}
```

{% endtab %}

{% tab title="Error Response (400)" %}

```typescript
{
  success: false,
  error: "Invalid JWT format or signature",
  data: null
}
```

{% endtab %} {% endtabs %}
