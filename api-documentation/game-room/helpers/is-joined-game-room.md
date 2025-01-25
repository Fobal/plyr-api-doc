---
description: Check if a player has joined a game room
---

# Check If Joined Game Room

{% hint style="info" %} Checks if a specific player has joined a game room. {% endhint %}

**Endpoint:** `/game/isJoined`  
**Method:** GET

{% tabs %} {% tab title="Request Parameters" %}

```typescript
{
    roomId: string; // The ID of the room to check
    plyrId: string; // The player ID to check
}
```

{% endtab %}

{% tab title="Success Response (200)" %}

```typescript
{
    success: true,
    data: {
        isJoined: boolean; // true if player has joined the room, false otherwise
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
const hmac = generateHmacSignature(timestamp, {}, secretKey);

const response = await axios.get(apiEndpoint + '/game/isJoined?roomId=' + roomId + '&plyrId=' + plyrId, {
    headers: {
        apikey: apiKey,
        signature: hmac,
        timestamp: timestamp
    }
});

const isJoined = response.data.data.isJoined;
```
