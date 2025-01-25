---
description: Reveal Claiming Code endpoint documentation
---

# Reveal Claiming Code

{% hint style="info" %} Reveal the claiming code for an Instant PlayPass session. {% endhint %}

**Endpoint:** `/instantPlayPass/reveal/claimingCode`  
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
    sessionJwt: string; // IPP Session JWT token
}
```

{% endtab %}

{% tab title="Success Response (200)" %}

```typescript
{
  success: true,
  data: {
    claimingCode: string  // The revealed claiming code
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
