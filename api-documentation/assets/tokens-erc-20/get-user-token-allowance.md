---
description: Get user token allowance for a game
---

# Get User Token Allowance

{% hint style="info" %} Retrieves the current token allowance for a player in a specific game. {% endhint %}

**Endpoint:** `/game/allowance/{plyrId}/{gameId}/{token}`  
**Method:** GET

{% tabs %} {% tab title="Request Parameters" %}

```typescript
{
    plyrId: string; // The player ID
    gameId: string; // The game ID
    token: string; // Token name/symbol
}
```

{% endtab %}

{% tab title="Success Response (200)" %}

```typescript
{
    allowance: string; // Current token allowance amount
    expiresAt: string; // ISO timestamp when the allowance expires
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
const hmac = generateHmacSignature(timestamp, {}, secretKey);

const response = await axios.get(apiEndpoint + '/game/allowance/' + plyrId + '/' + gameId + '/' + tokenName, {
    headers: {
        apikey: apiKey,
        signature: hmac,
        timestamp: timestamp
    }
});

const allowance = response.data.data.allowance;
const expiresAt = response.data.data.expiresAt;
```
