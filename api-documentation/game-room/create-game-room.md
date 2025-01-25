---
description: Create a new game room
---

# Create Game Room

{% hint style="info" %} Creates a new game room with specified expiration time. {% endhint %}

**Endpoint:** `/game/create`  
**Method:** POST

{% tabs %} {% tab title="Request Parameters" %}

```typescript
{
    expiresIn?: number; // Room expiration time in seconds (default: 86400 - 24 hours)
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
        result: {
            roomId: string; // The created room ID
        }
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
    expiresIn: 86400 // 24 hours
};

const hmac = generateHmacSignature(timestamp, body, secretKey);

const response = await axios.post(apiEndpoint + '/game/create', body, {
    headers: {
        apikey: apiKey,
        signature: hmac,
        timestamp: timestamp
    }
});

// Check task status to get roomId
const taskId = response.data.task.id;
// Poll task status until not PENDING
```
