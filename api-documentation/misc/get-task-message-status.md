---
description: Get the status of a task message
---

# Get Task Message Status

{% hint style="info" %} Check the status of an asynchronous task message. {% endhint %}

**Endpoint:** `/task/status/{taskId}`  
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
    taskId: string;
    taskData: {
        '0': string;
        '1': {
            gameId: string;
            plyrIds?: string[];
            roomId?: string;
            expiresIn?: number; // in seconds and only for createGameRoom
        };
        result?: {
            gameId: string;
            roomId: string;
            roomAddress: string;
        };
    };
    status: 'SUCCESS' | 'PENDING' | 'FAILED' | 'TIMEOUT';
    hash: string;
    errorMessage?: string;
    completedAt: string;
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
