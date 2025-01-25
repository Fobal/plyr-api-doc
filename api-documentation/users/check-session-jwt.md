---
description: Check session JWT validity endpoint
---

# Check Session JWT

{% hint style="info" %} Verify if a session JWT is valid and get associated user information. {% endhint %}

**Endpoint:** `/auth/check`  
**Method:** POST

{% tabs %} {% tab title="Request Body" %}

```typescript
{
    sessionJwt: string;
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
  error: "Invalid JWT format",
  data: null
}
```

{% endtab %} {% endtabs %}
