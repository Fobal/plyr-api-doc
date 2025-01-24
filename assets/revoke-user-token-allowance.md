---
description: Revoke token spending allowance for a user
---

# Revoke User Token Allowance

{% hint style="info" %} Revoke token spending allowance for a specific user. {% endhint %}

**Endpoint:** `/tokens/revoke`  
**Method:** POST

{% tabs %} {% tab title="Request Body" %}

```typescript
{
  sessionJwt: string,   // User's session JWT
  tokenSymbol: string   // Token symbol to revoke
}
```

{% endtab %}

{% tab title="Success Response (200)" %}

```typescript
{
  success: true,
  data: {
    taskId: string
  }
}
```

{% endtab %}

{% tab title="Error Response (404)" %}

```typescript
{
  success: false,
  error: "Failed to revoke token allowance",
  data: null
}
```

{% endtab %} {% endtabs %}
