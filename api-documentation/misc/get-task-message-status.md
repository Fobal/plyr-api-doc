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
```

{% endtab %}

{% tab title="Error Response (404)" %}

```typescript
{
    error: string;
}
```

{% endtab %} {% endtabs %}

## Example Usage

```javascript
// Setup request parameters
const timestamp = Date.now().toString();
const taskId = 'task_abc123xyz789';

// Generate HMAC signature (empty body for GET request)
const hmac = generateHmacSignature(timestamp, {}, secretKey);

// Make the API request
const response = await axios.get(apiEndpoint + '/task/status/' + taskId, {
    headers: {
        apikey: apiKey,
        signature: hmac,
        timestamp: timestamp
    }
});
```

{% hint style="info" %} Tasks are asynchronous operations that may take some time to complete. Use this endpoint to check their status. {% endhint %}

{% hint style="warning" %} Task status should be polled at reasonable intervals (e.g., every 1-2 seconds) to avoid rate limiting. {% endhint %}
