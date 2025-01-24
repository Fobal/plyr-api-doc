---
description: Login endpoint documentation
---

# Login

{% hint style="info" %} Authenticate a user with their Plyr ID and OTP. {% endhint %}

**Endpoint:** `/user/login`  
**Method:** POST

{% tabs %} {% tab title="Request Body" %}

```typescript
{
  plyrId: string,      // Lowercase username
  otp: string,         // 2FA token
  expiresIn: number,   // Session duration in seconds (default: 86400 * 31)
  gameId: string       // Game identifier
}
```

{% endtab %}

{% tab title="Success Response (200)" %}

```typescript
{
  success: true,
  data: {
    sessionJwt: string
  }
}
```

{% endtab %}

{% tab title="Error Response (404)" %}

```typescript
{
  success: false,
  error: "Invalid credentials or OTP",
  data: null
}
```

{% endtab %} {% endtabs %}
