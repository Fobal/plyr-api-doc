---
description: Remove players from a game room
---

# Leave Game Room

{% hint style="info" %} Removes one or more players from an existing game room using their session JWTs. {% endhint %}

**Endpoint:** `/game/leave`  
**Method:** POST

{% tabs %} {% tab title="Request Parameters" %}

```typescript
{
    roomId: string; // The ID of the room to leave
    sessionJwts: string[]; // Array of session JWTs for players leaving the room
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
        // Additional task data
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
    sessionJwts: ['jwt1', 'jwt2'] // Can remove multiple players at once
};

const hmac = generateHmacSignature(timestamp, body, secretKey);

const response = await axios.post(apiEndpoint + '/game/leave', body, {
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
