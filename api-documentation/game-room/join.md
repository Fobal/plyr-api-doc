---
description: Join an existing game room
---

# Join Game Room

{% hint style="info" %} Add players to an existing game room. {% endhint %}

**Endpoint:** `/game/join`  
**Method:** POST

{% tabs %} {% tab title="Request Body" %}

```typescript
{
  roomId: string,
  sessionJwts: string[],  // Array of player session JWTs
  sync: boolean          // Whether to wait for task completion
}
```

{% endtab %}

{% tab title="Success Response (200)" %}

```typescript
{
    taskId: string;
}
```

{% endtab %}

{% tab title="Error Response (404)" %}

```typescript
{
  error: "Failed to join game room",
}
```

{% endtab %} {% endtabs %}
