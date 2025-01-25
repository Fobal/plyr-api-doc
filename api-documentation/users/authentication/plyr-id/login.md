---
description: User login endpoint
---

# Login

{% hint style="info" %} Authenticate a user and get a session JWT token. {% endhint %}

**Endpoint:** `/user/login`  
**Method:** POST

{% tabs %} {% tab title="Request Body" %}

```typescript
{
    plyrId: string;     // Player ID (lowercase)
    otp: string;        // 2FA token
    expiresIn?: number; // Session expiration in seconds (optional, defaults to 86400s/24hrs)
    gameId: string;     // Game identifier
}
```

{% endtab %}

{% tab title="Success Response (200)" %}

```typescript
{
  success: true,
  data: {
    sessionJwt: string,
    plyrId: string,
    nonce: string,
    gameId: string,
    primaryAddress: string,
    mirrorAddress: string
  }
}
```

{% endtab %}

{% tab title="Error Response (400)" %}

```typescript
{
  success: false,
  error: string,
  data: null
}
```

{% endtab %} {% endtabs %}
