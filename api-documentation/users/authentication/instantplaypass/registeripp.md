---
description: Register Instant PlayPass endpoint documentation
---

# Register Instant PlayPass

{% hint style="info" %} Register a new Instant PlayPass session with specified tokens. {% endhint %}

**Endpoint:** `/instantPlayPass/register`  
**Method:** POST

{% tabs %} {% tab title="Request Headers" %}

```typescript
{
  apikey: string,      // Your API key
  signature: string,   // HMAC signature
  timestamp: string    // Current timestamp
}
```

{% endtab %}

{% tab title="Request Body" %}

```typescript
{
  tokens: string[],    // Array of tokens (e.g. ['plyr', 'gamr'])
  sync?: boolean      // Optional sync flag
}
```

{% endtab %}

{% tab title="Success Response (200)" %}

```typescript
{
  success: true,
  task: {
    id: string,       // Task ID for checking status
    status: string    // Task status
  }
}
```

{% endtab %}

{% tab title="Error Response" %}

```typescript
{
  success: false,
  error: string,
  data: null
}
```

{% endtab %} {% endtabs %}
