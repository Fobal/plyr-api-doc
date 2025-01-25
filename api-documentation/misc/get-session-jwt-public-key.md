---
description: Get the public key for verifying session JWTs
---

# Get Session JWT Public Key

{% hint style="info" %} Retrieve the public key used for verifying session JWTs. {% endhint %}

**Endpoint:** `/auth/publicKey`  
**Method:** GET

{% tabs %} {% tab title="Success Response (200)" %}

```typescript
{
  success: true,
  data: {
    publicKey: string  // Public key in PEM format
  }
}
```

{% endtab %}

{% tab title="Error Response (404)" %}

```typescript
{
  success: false,
  error: "Failed to retrieve public key",
  data: null
}
```

{% endtab %} {% endtabs %}
