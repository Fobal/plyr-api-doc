---
description: Distribute tokens from a game room to players
---

# Earn Game Room

{% hint style="info" %} Distributes tokens from a game room to one or more players. {% endhint %}

**Endpoint:** `/game/earn`  
**Method:** POST

{% tabs %} {% tab title="Request Parameters" %}

```typescript
{
    roomId: string; // The ID of the room to distribute from
    plyrIds: string[]; // Array of player IDs to receive tokens
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
    distributions: {
        plyrId: string;
        token: string;
        amount: number;
    }
    [];
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

{% hint style="info" %} The arrays `plyrIds`, `tokens`, and `amounts` must have corresponding lengths. {% endhint %}

## Example Usage

```javascript
// Sync=true usage
const timestamp = Date.now().toString();
const body = {
    roomId: 'room123',
    plyrIds: ['player1', 'player2'], // Multiple players can receive tokens
    tokens: ['TOKEN1', 'TOKEN2'], // Different tokens can be distributed
    amounts: [100, 200], // Corresponding amounts for each token
    sync: true // or omit for task-based response
};

const hmac = generateHmacSignature(timestamp, body, secretKey);

const response = await axios.post(apiEndpoint + '/game/earn', body, {
    headers: {
        apikey: apiKey,
        signature: hmac,
        timestamp: timestamp
    }
});
```

{% hint style="info" %} The arrays `plyrIds`, `tokens`, and `amounts` must have corresponding lengths. For example, if distributing multiple tokens to a single player, repeat the plyrId in the array. {% endhint %}
