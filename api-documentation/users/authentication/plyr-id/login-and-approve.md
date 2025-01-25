---
description: User login with token approval endpoint
---

# Login and Approve

{% hint style="info" %} Authenticate a user and approve token spending in a single request. {% endhint %}

**Endpoint:** `/user/loginAndApprove`  
**Method:** POST

{% tabs %} {% tab title="Request Body" %}

```typescript
{
    plyrId: string;     // Player ID (lowercase)
    gameId: string;     // Game identifier
    otp: string;        // 2FA token
    token: string;      // Token name to approve
    amount: number;     // Amount to approve
    expiresIn?: number; // Session expiration in seconds (optional, defaults to 86400s/24hrs)
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
