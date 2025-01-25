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
    roomId: string; // The ID of the ended room
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

## Example Usage

```javascript
// Sync=true usage
const timestamp = Date.now().toString();
const body = {
    roomId: '123',
    sync: true // or omit for task-based response
};

const hmac = generateHmacSignature(timestamp, body, secretKey);

const response = await axios.post(apiEndpoint + '/game/end', body, {
    headers: {
        apikey: apiKey,
        signature: hmac,
        timestamp: timestamp
    }
});
```
