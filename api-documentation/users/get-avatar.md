---
description: Get user avatar endpoint
---

# Get Avatar

{% hint style="info" %} Retrieve a user's avatar image URL. {% endhint %}

**Endpoint:** `/user/avatar/{plyrId}`  
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
    avatarUrl: string
  }
}
```

{% endtab %}

{% tab title="Error Response (404)" %}

```typescript
{
  success: false,
  error: "Avatar not found",
  data: null
}
```

{% endtab %} {% endtabs %}
