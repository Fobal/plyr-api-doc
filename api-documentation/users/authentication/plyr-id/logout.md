---
description: Logout endpoint documentation
---

# Logout

{% hint style="info" %} End a user session. {% endhint %}

**Endpoint:** `/user/logout`  
**Method:** POST

{% tabs %} {% tab title="Request Body" %}

```typescript
{
    sessionJwt: string; // Active session JWT
}
```

{% endtab %}

{% tab title="Success Response (200)" %}

```typescript
{
    message: string;
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
const timestamp = Date.now().toString();
const body = {
    sessionJwt: 'eyJhbGciOiJFUzI1NiIsInR5cCI6IkpXVCJ9...' // Active session JWT
};

const hmac = generateHmacSignature(timestamp, body, secretKey);

const response = await axios.post(apiEndpoint + '/user/logout', body, {
    headers: {
        apikey: apiKey,
        signature: hmac,
        timestamp: timestamp
    }
});
```

{% hint style="info" %} After logout, the session JWT becomes invalid and cannot be used for further API calls. {% endhint %} {% hint style="warning" %} Always clean up session data in your application after a successful logout. {% endhint %}
