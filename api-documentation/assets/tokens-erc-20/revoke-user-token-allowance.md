---
description: Revoke user token allowance for a game
---

# Revoke User Token Allowance

{% hint style="info" %} Revokes a previously granted token allowance for a game. {% endhint %}

**Endpoint:** `/game/revoke`  
**Method:** POST

{% tabs %} {% tab title="Request Parameters" %}

```typescript
{
    plyrId: string; // The player ID
    gameId: string; // The game ID
    token: string; // Token name/symbol to revoke
    otp: string; // One-time password for authorization
}
```

{% endtab %}

{% tab title="Success Response (200)" %}

```typescript
{
    // Revocation details
}
```

{% endtab %}

{% tab title="Error Response (400)" %}

```typescript
{
    error: string;
    data: null;
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
    token: 'USDC', // Token to revoke
    otp: '123456' // One-time password
};

// Generate HMAC signature
const hmac = generateHmacSignature(timestamp, body, secretKey);

// Make the API request
const response = await axios.post(apiEndpoint + '/game/revoke', body, {
    headers: {
        apikey: apiKey,
        signature: hmac,
        timestamp: timestamp
    }
});
```
