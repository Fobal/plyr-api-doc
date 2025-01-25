---
description: User login endpoint
---

# Login

{% hint style="info" %} Authenticate a user and get a session JWT token. {% endhint %}

**Endpoint:** `/user/login`  
**Method:** POST

{% tabs %} {% tab title="Request Body" %}

```typescript
{
    plyrId: string;     // Player ID (lowercase)
    otp: string;        // 2FA token
    expiresIn?: number; // Session expiration in seconds (optional, defaults to 86400s/24hrs)
    gameId: string;     // Game identifier
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
    otp: '123456', // 2FA token from authenticator app
    expiresIn: 3600, // Session will expire in 1 hour
    gameId: 'game123' // Your game's identifier
};

const hmac = generateHmacSignature(timestamp, body, secretKey);

const response = await axios.post(apiEndpoint + '/user/login', body, {
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
```

{% hint style="warning" %} Store the session JWT securely and never expose it in client-side code or logs. {% endhint %} {% hint style="info" %} The session JWT is required for most API endpoints and should be included in the request headers. {% endhint %}
