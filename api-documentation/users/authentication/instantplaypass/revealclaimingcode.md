---
description: Reveal Claiming Code endpoint documentation
---

# Reveal Claiming Code

{% hint style="info" %} Reveal the claiming code for an Instant PlayPass session. {% endhint %}

**Endpoint:** `/instantPlayPass/reveal/claimingCode`  
**Method:** POST

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
    claimingCode: string; // The revealed claiming code
}
```

{% endtab %}

{% tab title="Error Response" %}

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
    sessionJwt: 'eyJhbGciOiJFUzI1NiIsInR5cCI6IkpXVCJ9...' // IPP Session JWT from registration
};

const hmac = generateHmacSignature(timestamp, body, secretKey);

const response = await axios.post(apiEndpoint + '/instantPlayPass/reveal/claimingCode', body, {
    headers: {
        apikey: apiKey,
        signature: hmac,
        timestamp: timestamp
    }
});

// Get the claiming code
const { claimingCode } = response.data;
```
