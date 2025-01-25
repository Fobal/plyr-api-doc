---
description: Get user's ZooGenes NFTs
---

# Get User ZooGenes

{% hint style="info" %} Retrieve the PLYR ZooGenes NFTs for a specific user. {% endhint %}

**Endpoint:** `/nft/avalanche/zoogenes/{plyrId}`  
**Method:** GET

{% tabs %} {% tab title="Request Parameters" %}

```typescript
{
    plyrId: string; // The user's PlyrId
}
```

{% endtab %}

{% tab title="Success Response (200)" %}

```typescript
{
  success: true,
  data: Array<{
    owner: string,
    uri: string,
    collection: string,
    quantity: string,
    tokenId: string,
    name: string,
    image: string,
    description: string,
    attributes: Array<{
      trait_type: string,
      display_type?: string,
      value: string | number,
      max_value?: number
    }>
  }>
}
```

{% endtab %}

{% tab title="Error Response (404)" %}

```typescript
{
  success: false,
  data: null
}
```

{% endtab %} {% endtabs %}
