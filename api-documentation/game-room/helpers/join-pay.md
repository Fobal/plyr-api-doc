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
    gameId: 'game123',
    roomId: 'room123',
    sessionJwts: ['jwt1', 'jwt2'], // Multiple players can join and pay
    tokens: ['TOKEN1', 'TOKEN2'], // Different tokens can be paid
    amounts: [100, 200] // Corresponding amounts for each token
};

const hmac = generateHmacSignature(timestamp, body, secretKey);

const response = await axios.post(apiEndpoint + '/game/joinPay', body, {
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

{% hint style="info" %} The arrays `sessionJwts`, `tokens`, and `amounts` must have corresponding lengths. The operation is atomic - if either joining or paying fails, the entire operation is rolled back. {% endhint %}
