---
description: Get user's token balance
---

# Get User Token Balance

{% hint style="info" %} Retrieve the token balance for a specific user. {% endhint %}

**Endpoint:** `/tokens/balance/{plyrId}/{tokenSymbol}`  
**Method:** GET

{% tabs %} {% tab title="Request Parameters" %}

```typescript
{
  plyrId: string,      // The player's unique identifier
  tokenSymbol: string  // The token symbol
}
```

{% endtab %}

{% tab title="Success Response (200)" %}

```typescript
{
  success: true,
  data: {
    balance: string,  // Token balance as string
    decimals: number // Token decimals
  }
}
```

{% endtab %}

{% tab title="Error Response (404)" %}

```typescript
{
  success: false,
  error: "Failed to retrieve token balance",
  data: null
}
```

{% endtab %} {% endtabs %}
