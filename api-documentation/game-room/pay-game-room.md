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
        // Additional payment details
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
    sessionJwts: ['jwt1', 'jwt2'], // Multiple players can pay simultaneously
    tokens: ['TOKEN1', 'TOKEN2'], // Different tokens can be paid
    amounts: [100, 200] // Corresponding amounts for each token
};

const hmac = generateHmacSignature(timestamp, body, secretKey);

const response = await axios.post(apiEndpoint + '/game/pay', body, {
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

{% hint style="info" %} The arrays `sessionJwts`, `tokens`, and `amounts` must have corresponding lengths. For example, if paying with multiple tokens for a single player, repeat the sessionJwt in the array. {% endhint %}
