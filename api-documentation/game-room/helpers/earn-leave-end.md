---
description: Distribute earnings, remove players and end game room in one call
---

# Earn, Leave and End

{% hint style="info" %} Distribute earnings, remove players, and close the game room in one operation. {% endhint %}

**Endpoint:** `/game/earnLeaveEnd`  
**Method:** POST

{% tabs %} {% tab title="Request Body" %}

```typescript
{
  roomId: string,          // Game room identifier
  plyrIds: string[],       // Array of player IDs
  tokens: string[],        // Array of token names
  amounts: number[],       // Array of amounts to distribute
  sync: boolean           // Whether to wait for task completion
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
  error: "Failed to complete game room operations",
  data: null
}
```

{% endtab %} {% endtabs %}
