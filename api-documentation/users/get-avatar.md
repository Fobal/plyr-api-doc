---
description: Get multiple users' avatars endpoint
---

# Get Avatars

{% hint style="info" %} Retrieve avatar image URLs for multiple users. {% endhint %}

**Endpoint:** `/user/avatar`  
**Method:** POST

{% tabs %} {% tab title="Request Body" %}

```typescript
{
    plyrIds: string[]; // Array of player unique identifiers
}
```

{% endtab %}

{% tab title="Success Response (200)" %}

```typescript
{
  avatars: {
      [plyrId: string]: string // Map of plyrId to avatarUrl
    }
 }
```

{% endtab %}

{% tab title="Error Response (400)" %}

```typescript
{
  error: "Invalid request format",
  data: null
}
```

{% endtab %} {% endtabs %}

{% hint style="info" %} This endpoint is optimized for retrieving single or multiple avatars in a single request. {% endhint %}

## Example Usage

```javascript
const timestamp = Date.now().toString();
const body = {
    plyrIds: ['player123', 'player456', 'player789'] // Array of PLYR IDs
};

const hmac = generateHmacSignature(timestamp, body, secretKey);

const response = await axios.post(apiEndpoint + '/user/avatar', body, {
    headers: {
        apikey: apiKey,
        signature: hmac,
        timestamp: timestamp
    }
});

// Response will contain avatar URLs for each PLYR ID
const { avatars } = response.data;

// Process avatar URLs
Object.entries(avatars).forEach(([plyrId, avatarUrl]) => {
    console.log(`Avatar URL for ${plyrId}:`, avatarUrl);
    // Use avatarUrl in your application (e.g., display avatar image)
});
```
