---
description: Get user balance endpoint
---

# Get User Balance

{% hint style="info" %} Retrieve token balance for a user. Can query by PLYR ID or primary wallet address. {% endhint %}

**Endpoint:** `/user/balance/{identifier}/{tokenName?}`  
**Method:** GET

{% tabs %} {% tab title="Request Parameters" %}

```typescript
{
    identifier: string;  // PLYR ID or primary wallet address
    tokenName?: string; // Optional token name filter
}
```

{% endtab %}

{% tab title="Success Response (200)" %}

```typescript
{
  success: true,
  data: {
    balances: {
      [tokenName: string]: string // Map of token name to balance
    }
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
