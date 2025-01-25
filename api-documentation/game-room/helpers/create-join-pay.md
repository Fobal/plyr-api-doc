---
description: Create room, join players and process payment in one call
---

# Create, Join and Pay

{% hint style="info" %} Create a game room, join players, and process payment in one operation. {% endhint %}

**Endpoint:** `/game/createJoinPay`  
**Method:** POST

{% tabs %} {% tab title="Request Body" %}

```typescript
{
  expiresIn: number,        // Duration in seconds (default: 86400)
  sessionJwts: string[],    // Array of player session JWTs
  tokens: string[],         // Array of token names
  amounts: string[],        // Array of bet amounts
  sync: boolean            // Whether to wait for task completion
}
```

{% endtab %}

{% tab title="Success Response (200)" %}

```typescript
{
  success: true,
  data: {
    roomId: string,
    taskId: string
  }
}
```

{% endtab %}

{% tab title="Error Response (404)" %}

```typescript
{
  success: false,
  error: "Failed to create and setup game room",
  data: null
}
```

{% endtab %} {% endtabs %}
