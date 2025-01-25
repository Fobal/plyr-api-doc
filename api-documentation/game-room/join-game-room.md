---
description: Join players to a game room
---

# Join Game Room

{% hint style="info" %} Adds one or more players to an existing game room using their session JWTs. {% endhint %}

**Endpoint:** `/game/join`  
**Method:** POST

{% tabs %} {% tab title="Request Parameters" %}

```typescript
{
    roomId: string; // The ID of the room to join
    sessionJwts: string[]; // Array of session JWTs for players joining the room
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
    plyrIds: string[]; // Array of player IDs that joined
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
// Task=true usage
const timestamp = Date.now().toString();
const body = {
    roomId: '123',
    sessionJwts: ['jwt1', 'jwt2'], // Can add multiple session JWTs
    sync: true // or omit for task-based response
};

const hmac = generateHmacSignature(timestamp, body, secretKey);

const response = await axios.post(apiEndpoint + '/game/join', body, {
    headers: {
        apikey: apiKey,
        signature: hmac,
        timestamp: timestamp
    }
});
```
