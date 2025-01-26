---
description: Welcome to PLYR API documentation ❤️ bla bla some intro...
layout:
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: false
---

# Introduction

## Base Headers

Every API request must include these base headers:

```typescript
{
    apikey: string; // Your API key obtained from the developer portal
    signature: string; // HMAC signature of the request
    timestamp: string; // Current timestamp in milliseconds (Date.now().toString())
}
```

## Header Requirements

Format Requirements:

```
- Headers are case-sensitive
- Values must be strings
- Timestamp must be in milliseconds
```

## HMAC Signature Generation

```typescript
// Example signature generation
const timestamp = Date.now().toString();
const payload = JSON.stringify(requestBody);
const message = timestamp + payload;
const signature = crypto.createHmac('sha256', secretKey).update(message).digest('hex');
```

{% hint style="warning" %}
Always keep your API key and secret key secure. Never expose them in client-side code or public repositories.
{% endhint %}
