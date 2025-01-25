---
description: Register Instant PlayPass endpoint documentation
---

# Register Instant PlayPass

{% hint style="info" %} Register a new Instant PlayPass session with specified tokens. {% endhint %}

**Endpoint:** `/instantPlayPass/register`  
**Method:** POST

{% tabs %} {% tab title="Request Headers" %}

```typescript
{
  apikey: string,      // Your API key
  signature: string,   // HMAC signature
  timestamp: string    // Current timestamp
}
```

{% endtab %}

{% tab title="Request Body" %}

```typescript
{
  tokens: string[],    // Array of tokens (e.g. ['plyr', 'gamr'])
  sync?: boolean      // Optional sync flag
}
```

{% endtab %}

{% tab title="Success Response (200)" %}

```typescript
{
    sessionJwt: string,    // Session JWT token
    plyrId: string,        // Player ID
    gameId: string,        // Game ID
    primaryAddress: string, // Primary wallet address
    mirrorAddress: string, // Mirror wallet address
    avatar: string,        // Avatar URL
    ippClaimed: boolean,   // Whether IPP is claimed
    isIPP: boolean        // Whether this is an IPP session
}
```

{% endtab %}

{% tab title="Error Response" %}

```typescript
{
  error: string,
  data: null
}
```

{% endtab %} {% endtabs %}

{% hint style="info" %} After successful registration, use the "Reveal Claiming Code" endpoint to get the code for the user. {% endhint %} {% hint style="warning" %} Token synchronization may take additional time when the sync flag is enabled. {% endhint %}

## Example Usage

```javascript
const timestamp = Date.now().toString();
const body = {
    tokens: ['plyr', 'gamr'], // Tokens to include in the PlayPass
    sync: true // Optional: synchronize tokens
};

const hmac = generateHmacSignature(timestamp, body, secretKey);

const response = await axios.post(apiEndpoint + '/instantPlayPass/register', body, {
    headers: {
        apikey: apiKey,
        signature: hmac,
        timestamp: timestamp
    }
});

// Use the session JWT from the response
const sessionJwt = response.data.sessionJwt;

// You can now proceed with revealing the claiming code using the sessionJwt
```
