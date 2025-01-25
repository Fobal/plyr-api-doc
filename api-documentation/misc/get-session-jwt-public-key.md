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
    publicKey: string; // Base64 encoded public key
}
```

{% endtab %}

{% tab title="Error Response (400)" %}

```typescript
{
  error: string,
  data: null
}
```

{% endtab %} {% endtabs %}

## Example Usage

```typescript
// Fetch the public key
const response = await axios.get(apiEndpoint + '/jwt/publicKey');
const publicKey = response.data.publicKey;

// Verify a JWT locally
const decodedToken = jwt.verify(token, Buffer.from(publicKey, 'base64').toString('utf-8'), { algorithms: ['ES256'] });
```

{% hint style="info" %} The public key can be used to verify session JWTs locally without making API calls. {% endhint %}

{% hint style="warning" %} Cache the public key and reuse it for multiple verifications. Only fetch a new key if verification fails. {% endhint %}
