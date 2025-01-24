---
description: Distribute earnings and remove players from game room
---

# Earn and Leave

{% hint style="info" %} Distribute earnings and remove players from a game room. {% endhint %}

**Endpoint:** `/game/earnLeave`  
**Method:** POST

{% tabs %} {% tab title="Request Body" %}

```typescript
{
  roomId: string,
  plyrIds: string[],    // Array of player IDs
  tokens: string[],     // Array of token names
  amounts: number[],    // Array of amounts to distribute
  sync: boolean        // Whether to wait for task completion
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
  error: "Failed to process earnings and leave",
  data: null
}
```

{% endtab %} {% endtabs %}
