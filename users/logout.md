---
description: Logout endpoint documentation
---

# Logout

{% hint style="info" %} End a user session. {% endhint %}

**Endpoint:** `/user/logout`  
**Method:** POST

{% tabs %} {% tab title="Request Body" %}

```typescript
{
    sessionJwt: string; // Active session JWT
}
```

{% endtab %}

{% tab title="Success Response (200)" %}

```typescript
{
  success: true,
  data: {
    message: "Successfully logged out"
  }
}
```

{% endtab %}

{% tab title="Error Response (404)" %}

```typescript
{
  success: false,
  error: "Invalid session token",
  data: null
}
```

{% endtab %} {% endtabs %}
