---
description: Verify Claiming Code endpoint documentation
---

# VerifyClaimingCode

{% hint style="info" %}
Verify the validity of an Instant PlayPass claiming code.
{% endhint %}

**Endpoint:** `/instantPlayPass/verify/claimingCode/{claimingCode}`\
**Method:** GET

{% tabs %}
{% tab title="Request Parameters" %}
```typescript
{
    claimingCode: string; // The claiming code to verify
}
```
{% endtab %}

{% tab title="Success Response (200)" %}
```typescript
{
    valid: boolean; // Whether the claiming code is valid
    status: string; // Status of the claiming code
}
```
{% endtab %}

{% tab title="Error Response" %}
```typescript
{
    error: string;
}
```
{% endtab %}
{% endtabs %}

## Example Usage

```javascript
const timestamp = Date.now().toString();
const claimingCode = 'ABC123XYZ'; // The claiming code to verify

// Since this is a GET request with no body, pass null as the body for HMAC
const hmac = generateHmacSignature(timestamp, null, secretKey);

const response = await axios.get(apiEndpoint + `/instantPlayPass/verify/claimingCode/${claimingCode}`, {
    headers: {
        apikey: apiKey,
        signature: hmac,
        timestamp: timestamp
    }
});

// Check the validity and status of the claiming code
const { valid, status } = response.data;

if (valid) {
    console.log('Claiming code is valid');
    console.log('Status:', status);
    // Proceed with the claiming process
} else {
    console.log('Claiming code is invalid or expired');
    // Handle invalid code (e.g., ask user to try again)
}
```

{% hint style="warning" %}
Claiming codes can only be used once.
{% endhint %}
