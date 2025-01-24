---
description: Create a new game room
---

# Create Game Room

{% hint style="info" %} Create a new game room for players. {% endhint %}

**Endpoint:** `/game/create`  
**Method:** POST

{% tabs %} {% tab title="Request Body" %}

```typescript
{
  expiresIn: number,    // Duration in seconds (default: 86400)
  sync: boolean         // Whether to wait for task completion
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
  error: "Failed to create game room",
  data: null
}
```

{% endtab %} {% endtabs %}
