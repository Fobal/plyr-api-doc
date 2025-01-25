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
    roomId: string; // The created room ID
    roomAddress: string; // The room's blockchain address
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

## Example Usage

```javascript
// Sync=true usage
const timestamp = Date.now().toString();
const body = {
    expiresIn: 3600, // Room will expire in 1 hour
    sync: true // or omit for task-based response
};

const hmac = generateHmacSignature(timestamp, body, secretKey);

const response = await axios.post(apiEndpoint + '/game/create', body, {
    headers: {
        apikey: apiKey,
        signature: hmac,
        timestamp: timestamp
    }
});
```
