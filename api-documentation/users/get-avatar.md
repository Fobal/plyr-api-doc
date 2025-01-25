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
  success: true,
  data: {
    avatars: {
      [plyrId: string]: string // Map of plyrId to avatarUrl
    }
  }
}
```

{% endtab %}

{% tab title="Error Response (400)" %}

```typescript
{
  success: false,
  error: "Invalid request format",
  data: null
}
```

{% endtab %} {% endtabs %}
