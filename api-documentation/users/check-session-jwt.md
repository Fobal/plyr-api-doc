---
description: Check session JWT validity endpoint
---

# Check Session JWT

{% hint style="info" %} Verify if a session JWT is valid and get associated user information. {% endhint %}

**Endpoint:** `/user/session/verify`  
**Method:** POST

{% tabs %} {% tab title="Request Body" %}

```typescript
{
    sessionJwt: string; // JWT token to verify
}
```

{% endtab %}

{% tab title="Success Response (200)" %}

```typescript
{
  success: true,
  data: {
    isValid: boolean,
    plyrId?: string,
    walletAddress?: string
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
