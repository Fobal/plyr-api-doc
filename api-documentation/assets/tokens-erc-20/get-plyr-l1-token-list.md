---
description: Get list of available PLYR L1 tokens
---

# Get PLYR L1 Token List

{% hint style="info" %}
Retrieve the list of available PLYR L1 tokens.
{% endhint %}

**Endpoint:** `/tokens/tokenlist`\
**Method:** GET

{% tabs %}
{% tab title="Success Response (200)" %}
```typescript
{
  success: true,
  data: {
    tokens: Array<{
      name: string,
      symbol: string,
      decimals: number,
      address: string
    }>
  }
}
```
{% endtab %}

{% tab title="Error Response (404)" %}
```typescript
{
  success: false,
  error: "Failed to retrieve token list",
  data: null
}
```
{% endtab %}
{% endtabs %}
