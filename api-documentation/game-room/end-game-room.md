---
description: End a game room session
---

# End Game Room

{% hint style="info" %} Ends a game room session and cleans up associated resources. {% endhint %}

**Endpoint:** `/game/end`  
**Method:** POST

{% tabs %} {% tab title="Request Parameters" %}

```typescript
{
    roomId: string; // The ID of the room to end
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
    roomId: 'room123'
};

const hmac = generateHmacSignature(timestamp, body, secretKey);

const response = await axios.post(apiEndpoint + '/game/end', body, {
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
