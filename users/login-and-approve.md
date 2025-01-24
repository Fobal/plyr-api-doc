---
description: Login and approve endpoint documentation
---

# Login and Approve

{% hint style="info" %} Authenticate a user and approve token spending in a single request. {% endhint %}

**Endpoint:** `/user/login-and-approve`  
**Method:** POST

{% tabs %} {% tab title="Request Body" %}

```typescript
{
  plyrId: string,      // Lowercase username
  otp: string,         // 2FA token
  expiresIn: number,   // Session duration in seconds (default: 86400 * 31)
  gameId: string,      // Game identifier
  tokenAddress: string // Address of the token to approve
}
```

{% endtab %}

{% tab title="Success Response (200)" %}

```typescript
{
  success: true,
  data: {
    sessionJwt: string,
    approvalTx: string // Transaction hash of the approval
  }
}
```

{% endtab %}

{% tab title="Error Response (404)" %}

```typescript
{
  success: false,
  error: "Invalid credentials, OTP, or token address",
  data: null
}
```

{% endtab %} {% endtabs %}
