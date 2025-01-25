---
description: Check session JWT validity endpoint
---

# Check Session JWT

{% hint style="info" %} Verify if a session JWT is valid and get associated user information. {% endhint %}

**Endpoint:** `/user/session/verify`  
**Method:** POST

{% tabs %} {% tab title="Request Body" %}

```typescript
{
    sessionJwt: string; // JWT token to verify
}
```

{% endtab %}

{% tab title="Success Response (200)" %}

```typescript
{
  isValid: boolean,
    plyrId?: string,
    walletAddress?: string
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

{% hint style="info" %} For local JWT verification without making an API call, see the "Verify JWT Locally" documentation. {% endhint %} {% hint style="warning" %} Session JWTs have an expiration time. Always verify JWTs before using them in critical operations. {% endhint %}

## Example Usage

```javascript
const timestamp = Date.now().toString();
const body = {
    sessionJwt: 'eyJhbGciOiJFUzI1NiIsInR5cCI6IkpXVCJ9...' // JWT to verify
};

const hmac = generateHmacSignature(timestamp, body, secretKey);

const response = await axios.post(apiEndpoint + '/user/session/verify', body, {
    headers: {
        apikey: apiKey,
        signature: hmac,
        timestamp: timestamp
    }
});
```
