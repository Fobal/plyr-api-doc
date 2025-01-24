---
description: Get the status of a task message
---

# Get Task Message Status

{% hint style="info" %} Check the status of an asynchronous task message. {% endhint %}

**Endpoint:** `/task/{taskId}`  
**Method:** GET

{% tabs %} {% tab title="Request Parameters" %}

```typescript
{
    taskId: string; // The task's unique identifier
}
```

{% endtab %}

{% tab title="Success Response (200)" %}

```typescript
{
  success: true,
  data: {
    status: 'pending' | 'completed' | 'failed',
    result?: any,
    error?: string,
    progress?: number
  }
}
```

{% endtab %}

{% tab title="Error Response (404)" %}

```typescript
{
  success: false,
  error: "Task not found",
  data: null
}
```

{% endtab %} {% endtabs %}
