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
  plyrId: string,
    username: string,
    walletAddress: string,
    avatarUrl: string
 }
```

{% endtab %}

{% tab title="Error Response (404)" %}

```typescript
{
  error: "User not found",
  data: null
}
```

{% endtab %} {% endtabs %}

## Example Usage

```javascript
const timestamp = Date.now().toString();
// Can use either PLYR ID or wallet address
const identifier = 'player123'; // or '0x742d35Cc6634C0532925a3b844Bc454e4438f44e'

// Since this is a GET request with no body, pass null as the body for HMAC
const hmac = generateHmacSignature(timestamp, null, secretKey);

const response = await axios.get(apiEndpoint + `/user/info/${identifier}`, {
    headers: {
        apikey: apiKey,
        signature: hmac,
        timestamp: timestamp
    }
});

// Response will contain basic user information
const { plyrId, username, walletAddress, avatarUrl } = response.data;
```

{% hint style="info" %} The identifier can be either a PLYR ID or a wallet address. The API will automatically detect which type it is and return the corresponding user information. {% endhint %}
