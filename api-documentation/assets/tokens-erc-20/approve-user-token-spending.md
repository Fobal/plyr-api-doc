---
description: Approve user token spending for a game
---

# Approve User Token Spending

{% hint style="info" %} Approves a specific amount of tokens for use in a game. {% endhint %}

**Endpoint:** `/game/approve`  
**Method:** POST

{% tabs %} {% tab title="Request Parameters" %}

```typescript
{
    plyrId: string; // The player ID
    gameId: string; // The game ID
    otp: string; // One-time password for authorization
    token: string; // Token name/symbol
    amount: number; // Amount to approve
    expiresIn: number; // Approval expiration time in seconds
}
```

{% endtab %}

{% tab title="Success Response (200)" %}

```typescript
{
    // Approval details
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
// Setup request parameters
const timestamp = Date.now().toString();
const body = {
    plyrId: 'player_abc123', // The player's ID
    gameId: 'game_xyz789', // The game's ID
    otp: '123456', // One-time password
    token: 'USDC', // Token to approve
    amount: 1000, // Amount to approve (in token's smallest unit)
    expiresIn: 3600 // Approval expires in 1 hour
};

// Generate HMAC signature
const hmac = generateHmacSignature(timestamp, body, secretKey);

// Make the API request
const response = await axios.post(apiEndpoint + '/game/approve', body, {
    headers: {
        apikey: apiKey,
        signature: hmac,
        timestamp: timestamp
    }
});
```
