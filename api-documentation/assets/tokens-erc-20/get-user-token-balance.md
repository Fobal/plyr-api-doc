---
description: Get user balance endpoint
---

# Get User Token Balance

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
  balances: {
      [tokenName: string]: string // Map of token name to balance
    }
 }
```

{% endtab %}

{% tab title="Error Response (404)" %}

```typescript
{
  error: "User not found",
}
```

{% endtab %} {% endtabs %}

{% hint style="info" %} If no token name is provided, the endpoint returns balances for all tokens the user holds. {% endhint %}

## Example Usage

```javascript
const timestamp = Date.now().toString();
// Can use either PLYR ID or wallet address
const identifier = 'player123'; // or '0x742d35Cc6634C0532925a3b844Bc454e4438f44e'
const tokenName = 'TOKEN1'; // Optional: specific token to query

// Since this is a GET request with no body, pass null as the body for HMAC
const hmac = generateHmacSignature(timestamp, null, secretKey);

// Build URL based on whether tokenName is provided
const url = `/user/balance/${identifier}/${tokenName}`;

const response = await axios.get(apiEndpoint + url, {
    headers: {
        apikey: apiKey,
        signature: hmac,
        timestamp: timestamp
    }
});

// Response will contain token balances
const { balances } = response.data;

// Process balances
Object.entries(balances).forEach(([tokenName, balance]) => {
    console.log(`Balance for ${tokenName}:`, balance);
    // Use balances in your application
});
```
