---
description: Get basic user information endpoint
---

# Get Basic User Info

{% hint style="info" %} Retrieve basic information about a user. {% endhint %}

**Endpoint:** `/user/basic/{plyrId}`  
**Method:** GET

{% tabs %} {% tab title="Request Parameters" %}

```typescript
{
    plyrId: string; // The player's unique identifier
}
```

{% endtab %}

{% tab title="Success Response (200)" %}

```typescript
{
  success: true,
  data: {
    plyrId: string,
    username: string,
    walletAddress: string,
    avatarUrl: string
  }
}
```

{% endtab %}

{% tab title="Error Response (404)" %}

```typescript
{
  success: false,
  error: "User not found",
  data: null
}
```

{% endtab %} {% endtabs %}
