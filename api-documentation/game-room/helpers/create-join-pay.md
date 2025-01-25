---
description: Create a game room, join players, and process payments in a single operation
---

# Create Join Pay

{% hint style="info" %} Combines creating a game room, joining players, and processing payments into a single atomic operation. {% endhint %}

**Endpoint:** `/game/createJoinPay`  
**Method:** POST

{% tabs %} {% tab title="Request Parameters" %}

```typescript
{
    sessionJwts: string[]; // Array of session JWTs for players to join and pay
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
        result: {
            roomId: string; // The created room ID
        }
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
    sessionJwts: ['jwt1', 'jwt2'], // Multiple players can join and pay
    tokens: ['TOKEN1', 'TOKEN2'], // Different tokens can be paid
    amounts: [100, 200] // Corresponding amounts for each token
};

const hmac = generateHmacSignature(timestamp, body, secretKey);

const response = await axios.post(apiEndpoint + '/game/createJoinPay', body, {
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

{% hint style="info" %} The arrays `sessionJwts`, `tokens`, and `amounts` must have corresponding lengths. The operation is atomic - if any step (create, join, or pay) fails, the entire operation is rolled back. {% endhint %}
