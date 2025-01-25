---
description: Get user activity logs
---

# Activity Logs

{% hint style="info" %}
Retrieve activity logs for a specific user.
{% endhint %}

**Endpoint:** `/activityLogs/{plyrId}`\
**Method:** GET

{% tabs %}
{% tab title="Request Parameters" %}
```typescript
{
  plyrId: string,     // The player's unique identifier
  startTime?: number, // Start timestamp (optional)
  endTime?: number,   // End timestamp (optional)
  limit?: number      // Maximum number of logs to return (optional)
}
```
{% endtab %}

{% tab title="Success Response (200)" %}
```typescript
{
    logs: Array<{
        timestamp: number;
        action: string;
        details: {
            [key: string]: any;
        };
    }>;
}
```
{% endtab %}

{% tab title="Error Response (400)" %}
```typescript
{
  error: "Failed to retrieve activity logs",
  data: null
}
```
{% endtab %}
{% endtabs %}
