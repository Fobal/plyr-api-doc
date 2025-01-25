---
description: Get user's NFT collection
---

# Get User NFTs

{% hint style="info" %} Retrieve the NFT collection for a specific user. {% endhint %}

**Endpoint:** `/nfts/{plyrId}`  
**Method:** GET

{% tabs %} {% tab title="Request Parameters" %}

```typescript
{
    plyrId: string; // The player's unique identifier
}
```

{% endtab %}

{% tab title="Success Response (200)" %}

```typescript
{
  success: true,
  data: {
    nfts: Array<{
      tokenId: string,
      contractAddress: string,
      metadata: {
        name: string,
        description: string,
        image: string,
        attributes: Array<{
          trait_type: string,
          value: string | number
        }>
      }
    }>
  }
}
```

{% endtab %}

{% tab title="Error Response (404)" %}

```typescript
{
  success: false,
  error: "Failed to retrieve NFTs",
  data: null
}
```

{% endtab %} {% endtabs %}
