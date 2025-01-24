---
description: Join game room and process payment in one call
---

# Join and Pay

{% hint style="info" %} Join a game room and process payment in one operation. {% endhint %}

**Endpoint:** `/game/joinPay`  
**Method:** POST

{% tabs %} {% tab title="Request Body" %}

```typescript
{
  roomId: string,
  sessionJwts: string[],  // Array of player session JWTs
  tokens: string[],       // Array of token names
  amounts: string[],      // Array of amounts
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
  error: "Failed to join and pay",
  data: null
}
```

{% endtab %} {% endtabs %}
