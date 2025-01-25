---
description: Distribute tokens and remove players from a game room in a single operation
---

# Earn Leave

{% hint style="info" %} Combines distributing tokens to players and removing them from a game room into a single atomic operation. {% endhint %}

**Endpoint:** `/game/earnLeave`  
**Method:** POST

{% tabs %} {% tab title="Request Parameters" %}

```typescript
{
    roomId: string; // The ID of the room
    plyrIds: string[]; // Array of player IDs to receive tokens and leave
    tokens: string[]; // Array of token names/symbols
    amounts: number[]; // Array of amounts to distribute (corresponding to tokens array)
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
        plyrIds: string[]; // Array of player IDs that received tokens and left
        distributions: {
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
}
```

{% endtab %} {% endtabs %}

{% hint style="info" %} The arrays `plyrIds`, `tokens`, and `amounts` must have corresponding lengths. The operation is atomic - if either earning or leaving fails, the entire operation is rolled back. {% endhint %}

## Example Usage

```javascript
// Sync=true usage
const timestamp = Date.now().toString();
const body = {
    roomId: '123',
    plyrIds: ['player1', 'player1', 'player2'], // First player receiving 2 tokens, second player receiving 1
    tokens: ['TOKEN1', 'TOKEN2', 'TOKEN1'], // Token types to distribute
    amounts: [100, 50, 75], // Corresponding amounts
    sync: true // or omit for task-based response
};

const hmac = generateHmacSignature(timestamp, body, secretKey);

const response = await axios.post(apiEndpoint + '/game/earnLeave', body, {
    headers: {
        apikey: apiKey,
        signature: hmac,
        timestamp: timestamp
    }
});
```
