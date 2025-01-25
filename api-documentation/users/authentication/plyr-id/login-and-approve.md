---
description: User login with token approval endpoint
---

# Login and Approve

{% hint style="info" %} Authenticate a user and approve token spending in a single request. {% endhint %}

**Endpoint:** `/user/loginAndApprove`  
**Method:** POST

{% tabs %} {% tab title="Request Body" %}

```typescript
{
    plyrId: string;     // Player ID (lowercase)
    gameId: string;     // Game identifier
    otp: string;        // 2FA token
    tokens: string[];      // Token names to approve
    amounts: number[];     // Amounts to approve
    expiresIn?: number; // Session expiration in seconds (optional, defaults to 86400s/24hrs)
}
```

{% endtab %}

{% tab title="Success Response (200)" %}

```typescript
{
  sessionJwt: string,
    plyrId: string,
    nonce: string,
    gameId: string,
    primaryAddress: string,
    mirrorAddress: string
 }
```

{% endtab %}

{% tab title="Error Response (400)" %}

```typescript
{
    error: string;
}
```

{% endtab %} {% endtabs %}

## Example Usage

```javascript
const timestamp = Date.now().toString();
const body = {
    plyrId: 'player123',
    gameId: 'game123',
    otp: '123456', // 2FA token from authenticator app
    tokens: ['TOKEN1', 'TOKEN2'], // Token names to approve for spending
    amounts: [1000, 2000], // Amounts to approve
    expiresIn: 3600 // Session will expire in 1 hour
};

const hmac = generateHmacSignature(timestamp, body, secretKey);

const response = await axios.post(apiEndpoint + '/user/loginAndApprove', body, {
    headers: {
        apikey: apiKey,
        signature: hmac,
        timestamp: timestamp
    }
});

// Store session information securely
const {
    sessionJwt, // JWT token for future API calls
    plyrId, // Player's ID
    nonce, // Unique nonce for this session
    gameId, // Game identifier
    primaryAddress, // User's primary wallet address
    mirrorAddress // User's mirror wallet address
} = response.data;

// Use sessionJwt for subsequent authenticated API calls
// Token approval is already processed
```

{% hint style="info" %} This endpoint combines login and token approval into a single atomic operation, making it more efficient than separate calls. {% endhint %} {% hint style="warning" %} Store the session JWT securely and never expose it in client-side code or logs. {% endhint %} {% hint style="warning" %} The approved amounts represent the maximum amounts that can be spent per token. The actual spending may be less. {% endhint %}
