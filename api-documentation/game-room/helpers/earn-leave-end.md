---
description: Distribute tokens, remove players, and end a game room in a single operation
---

# Earn Leave End

{% hint style="info" %} Combines distributing tokens to players, removing them from a game room, and ending the room into a single atomic operation. {% endhint %}

**Endpoint:** `/game/earnLeaveEnd`  
**Method:** POST

{% tabs %} {% tab title="Request Parameters" %}

```typescript
{
    roomId: string; // The ID of the room
    plyrIds: string[]; // Array of player IDs to receive tokens and leave
    tokens: string[]; // Array of token names/symbols
    amounts: number[]; // Array of amounts to distribute (corresponding to tokens array)
}
```

{% endtab %}

{% tab title="Success Response (200)" %}

```typescript
{
    success: true,
    data: {
        task: {
            id: string; // Task ID for checking status
        }
    }
}
```

After task completion:

```typescript
{
    taskData: {
        status: 'SUCCESS';
        // Additional operation details
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
    roomId: 'room123',
    plyrIds: ['player1', 'player2'], // Multiple players can earn and leave
    tokens: ['TOKEN1', 'TOKEN2'], // Different tokens can be distributed
    amounts: [100, 200] // Corresponding amounts for each token
};

const hmac = generateHmacSignature(timestamp, body, secretKey);

const response = await axios.post(apiEndpoint + '/game/earnLeaveEnd', body, {
    headers: {
        apikey: apiKey,
        signature: hmac,
        timestamp: timestamp
    }
});

// Check task status
const taskId = response.data.task.id;
// Poll task status until not PENDING
```

{% hint style="info" %} The arrays `plyrIds`, `tokens`, and `amounts` must have corresponding lengths. The operation is atomic - if any step (earn, leave, or end) fails, the entire operation is rolled back. {% endhint %}
