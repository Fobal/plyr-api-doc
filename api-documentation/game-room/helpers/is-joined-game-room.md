---
description: Check if a player has joined a specific game room
---

# Is Joined Game Room

{% hint style="info" %} Check if a player has joined a specific game room. {% endhint %}

**Endpoint:** `/game/isJoined/{roomId}/{plyrId}`  
**Method:** GET

{% tabs %} {% tab title="Request Parameters" %}

```typescript
{
  roomId: string,    // The ID of the game room
  plyrId: string     // The Plyr ID of the user
}
```

{% endtab %}

{% tab title="Success Response (200)" %}

```typescript
{
  success: true,
  data: {
    isJoined: boolean
  }
}
```

{% endtab %}

{% tab title="Error Response (404)" %}

```typescript
{
  success: false,
  error: "Failed to check game room status",
  data: null
}
```

{% endtab %} {% endtabs %}
