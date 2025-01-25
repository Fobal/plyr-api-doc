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
    success: true,
    data: {
        // Approval details
    }
}
```

{% endtab %}

{% tab title="Error Response (400)" %}

```typescript
{
    success: false,
    error: string;
    data: null;
}
```

{% endtab %} {% endtabs %}

## Example Usage

```javascript
const timestamp = Date.now().toString();
const body = {
    plyrId: 'player123',
    gameId: 'game123',
    otp: '123456',
    token: 'TOKEN',
    amount: 1000,
    expiresIn: 3600 // 1 hour
};

const hmac = generateHmacSignature(timestamp, body, secretKey);

const response = await axios.post(apiEndpoint + '/game/approve', body, {
    headers: {
        apikey: apiKey,
        signature: hmac,
        timestamp: timestamp
    }
});
```
