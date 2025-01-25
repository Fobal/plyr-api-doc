---
description: Get session JWT public key endpoint
---

# Get Session JWT Public Key

{% hint style="info" %} Retrieve the public key used to verify session JWTs locally. {% endhint %}

**Endpoint:** `/jwt/publicKey`  
**Method:** GET

{% tabs %} {% tab title="Request Body" %}

```typescript
// No request body required
```

{% endtab %}

{% tab title="Success Response (200)" %}

```typescript
{
  success: true,
  data: {
    publicKey: string  // Base64 encoded public key
  }
}
```

{% endtab %}

{% tab title="Error Response (400)" %}

```typescript
{
  success: false,
  error: string,
  data: null
}
```

{% endtab %} {% endtabs %}
