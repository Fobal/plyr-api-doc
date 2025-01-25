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
    plyrIds: string[]; // Array of player IDs that left
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
    sessionJwts: ['playerJwt1', 'playerJwt2'], // Multiple players can leave at once
    sync: true // or omit for task-based response
};

const hmac = generateHmacSignature(timestamp, body, secretKey);

const response = await axios.post(apiEndpoint + '/game/leave', body, {
    headers: {
        apikey: apiKey,
        signature: hmac,
        timestamp: timestamp
    }
});
```
