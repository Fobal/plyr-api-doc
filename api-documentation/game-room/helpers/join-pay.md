---
description: Join a game room and pay tokens in a single operation
---

# Join Pay

{% hint style="info" %} Combines joining a game room and paying tokens into a single atomic operation. {% endhint %}

**Endpoint:** `/game/joinPay`  
**Method:** POST

{% tabs %} {% tab title="Request Parameters" %}

```typescript
{
    gameId: string; // The game ID
    roomId: string; // The ID of the room to join and pay to
    sessionJwts: string[]; // Array of session JWTs for players joining and paying
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
        roomId: string;
        plyrIds: string[]; // Array of player IDs that joined
        payments: {
            plyrId: string;
            token: string;
            amount: number;
        }[];
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

{% hint style="info" %} The arrays `sessionJwts`, `tokens`, and `amounts` must have corresponding lengths. The operation is atomic - if either joining or paying fails, the entire operation is rolled back. {% endhint %}

## Example Usage

```javascript
// Sync=true usage
const timestamp = Date.now().toString();
const body = {
    gameId: 'game_xyz',
    roomId: '123',
    sessionJwts: ['playerJwt1', 'playerJwt2'],
    tokens: ['TOKEN1', 'TOKEN2'],
    amounts: [100, 50],
    sync: true // or omit for task-based response
};

const hmac = generateHmacSignature(timestamp, body, secretKey);

const response = await axios.post(apiEndpoint + '/game/joinPay', body, {
    headers: {
        apikey: apiKey,
        signature: hmac,
        timestamp: timestamp
    }
});
```
