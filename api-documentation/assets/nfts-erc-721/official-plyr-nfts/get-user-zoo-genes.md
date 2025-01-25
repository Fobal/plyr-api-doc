---
description: Get user's PLYR Zoo Genes NFTs
---

# Get User Zoo Genes

{% hint style="info" %} Retrieve the PLYR Zoo Genes NFTs for a specific user. {% endhint %}

**Endpoint:** `/nfts/zoo/{plyrId}`  
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
Array<{
    tokenId: string;
    metadata: {
        name: string;
        description: string;
        image: string;
        attributes: Array<{
            trait_type: string;
            value: string | number;
        }>;
        genes: {
            species: string;
            rarity: string;
            generation: number;
        };
    };
}>;
```

{% endtab %}

{% tab title="Error Response (404)" %}

```typescript
{
  error: "Failed to retrieve Zoo Genes NFTs",
}
```

{% endtab %} {% endtabs %}
