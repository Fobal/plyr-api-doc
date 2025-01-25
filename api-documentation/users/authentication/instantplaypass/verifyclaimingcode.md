---
description: Verify Claiming Code endpoint documentation
---

# Verify Claiming Code

{% hint style="info" %} Verify the validity of an Instant PlayPass claiming code. {% endhint %}

**Endpoint:** `/instantPlayPass/verify/claimingCode/{claimingCode}`  
**Method:** GET

{% tabs %} {% tab title="Request Headers" %}

```typescript
{
  apikey: string,      // Your API key
  signature: string,   // HMAC signature
  timestamp: string    // Current timestamp
}
```

{% endtab %}

{% tab title="Path Parameters" %}

```typescript
claimingCode: string; // The claiming code to verify
```

{% endtab %}

{% tab title="Success Response (200)" %}

```typescript
{
  success: true,
  data: {
    valid: boolean,     // Whether the claiming code is valid
    status: string      // Status of the claiming code
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
