---
description: Get user's token balance
---

# Get User Token Balance

{% hint style="info" %} Retrieve the token balance for a specific user using either PLYR ID or Primary address. {% endhint %}

**Endpoint:** `/user/balance/{searchTxt}/{tokenName?}`  
**Method:** GET

{% tabs %} {% tab title="Request Parameters" %}

```typescript
{
  searchTxt: string,   // The player's PLYR ID or Primary address
  tokenName?: string   // Optional token name parameter
}
```

{% endtab %}

{% tab title="Success Response (200)" %}

```typescript
{
  success: true,
  data: {
    balance: string,  // Token balance as string
    decimals: number  // Token decimals
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

**Examples:**

```typescript
// Using PLYR ID
/user/balance/tonnystripes
// Using Primary address
/user/balance/0x...
// With specific token
/user/balance/tonnystripes/USDT
```
