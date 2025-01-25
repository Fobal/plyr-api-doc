---
description: Get basic user information endpoint
---

# Get Basic User Info

{% hint style="info" %} Retrieve basic user information. Can query by PLYR ID or primary wallet address. {% endhint %}

**Endpoint:** `/user/info/{identifier}`  
**Method:** GET

{% tabs %} {% tab title="Request Parameters" %}

```typescript
{
    identifier: string; // PLYR ID or primary wallet address
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
