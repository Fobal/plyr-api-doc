---
description: Pay tokens to a game room
---

# Pay Game Room

{% hint style="info" %} Processes token payments from one or more players to a game room. {% endhint %}

**Endpoint:** `/game/pay`  
**Method:** POST

{% tabs %} {% tab title="Request Parameters" %}

```typescript
{
    roomId: string; // The ID of the room to pay to
    sessionJwts: string[]; // Array of session JWTs for players making payments
    tokens: string[]; // Array of token names/symbols
    amounts: number[]; // Array of amounts to pay (corresponding to tokens array)
    sync?: boolean; // When true, returns direct response. When false/undefined, returns a task ID for polling status
}
```

{% endtab %}

{% tab title="Success Response (200)" %}

When sync=false (default):

```typescript
{
    task: {
        id: string; // Task ID for checking status
    }
}
```

When sync=true:

```typescript
{
    // Payment details
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

{% hint style="info" %} The arrays `sessionJwts`, `tokens`, and `amounts` must have corresponding lengths. {% endhint %}

## Example Usage

```javascript
// Sync=true usage
const timestamp = Date.now().toString();
const body = {
    roomId: '123',
    sessionJwts: ['playerJwt1', 'playerJwt1', 'playerJwt2'], // First player paying 2 tokens, second player paying 1
    tokens: ['TOKEN1', 'TOKEN2', 'TOKEN1'], // Token types to pay
    amounts: [100, 50, 75], // Corresponding amounts
    sync: true // or omit for task-based response
};

const hmac = generateHmacSignature(timestamp, body, secretKey);

const response = await axios.post(apiEndpoint + '/game/pay', body, {
    headers: {
        apikey: apiKey,
        signature: hmac,
        timestamp: timestamp
    }
});
```
