---
description: Approve token spending allowance for a user
---

# Approve User Token Spending

{% hint style="info" %} Approve token spending allowance for a specific user. {% endhint %}

**Endpoint:** `/tokens/approve`  
**Method:** POST

{% tabs %} {% tab title="Request Body" %}

```typescript
{
  sessionJwt: string,   // User's session JWT
  tokenSymbol: string,  // Token symbol to approve
  amount: string       // Amount to approve as string
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
  error: "Failed to approve token spending",
  data: null
}
```

{% endtab %} {% endtabs %}
