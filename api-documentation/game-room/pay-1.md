---
description: Process payments for game room players
---

# Earn

{% hint style="info" %}
Process payments for players in a game room.
{% endhint %}

**Endpoint:** `/game/pay`\
**Method:** POST

{% tabs %}
{% tab title="Request Body" %}
```typescript
{
  roomId: string,
  sessionJwts: string[],  // Array of player session JWTs
  tokens: string[],       // Array of token names (one per player)
  amounts: string[],      // Array of amounts (one per player)
  sync: boolean          // Whether to wait for task completion
}
```
{% endtab %}

{% tab title="Success Response (200)" %}
```typescript
{
  success: true,
  data: {
    taskId: string
  }
}
```
{% endtab %}

{% tab title="Error Response (404)" %}
```typescript
{
  success: false,
  error: "Failed to process payment",
  data: null
}
```
{% endtab %}
{% endtabs %}
