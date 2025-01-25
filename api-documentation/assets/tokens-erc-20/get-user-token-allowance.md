---
description: Get user's token spending allowance
---

# Get User Token Allowance

{% hint style="info" %} Retrieve the token spending allowance for a specific user. {% endhint %}

**Endpoint:** `/tokens/allowance/{plyrId}/{tokenSymbol}`  
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
    allowance: string,  // Token allowance as string
    decimals: number   // Token decimals
  }
}
```

{% endtab %}

{% tab title="Error Response (404)" %}

```typescript
{
  success: false,
  error: "Failed to retrieve token allowance",
  data: null
}
```

{% endtab %} {% endtabs %}
