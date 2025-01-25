---
description: Get user's ZooGenes NFTs
---

# Get User Zoo Genes

{% hint style="info" %} Retrieve the PLYR ZooGenes NFTs for a specific user. {% endhint %}

**Endpoint:** `/nft/avalanche/zoogenes/{plyrId}`\
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
Array<{
    owner: string;
    uri: string;
    collection: string;
    quantity: string;
    tokenId: string;
    name: string;
    image: string;
    description: string;
    attributes: Array<{
        trait_type: string;
        display_type?: string;
        value: string | number;
        max_value?: number;
    }>;
}>;
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
const plyrId = 'player123';

// Since this is a GET request with no body, pass null as the body for HMAC
const hmac = generateHmacSignature(timestamp, null, secretKey);

// Make the API request
const response = await axios.get(apiEndpoint + `/nft/avalanche/zoogenes/${plyrId}`, {
    headers: {
        apikey: apiKey,
        signature: hmac,
        timestamp: timestamp
    }
});

// Response will contain array of ZooGene NFTs with their metadata
const zoogenes = response.data.data;
// Access individual ZooGene properties
zoogenes.forEach((nft) => {
    console.log(`ZooGene #${nft.tokenId}:`);
    console.log(`- Name: ${nft.name}`);
    console.log(`- Image: ${nft.image}`);
    console.log('- Attributes:', nft.attributes);
});
```

{% hint style="info" %} ZooGenes are special NFTs with unique attributes that can be used in various PLYR games and experiences. [https://opensea.io/collection/zoogenes](https://opensea.io/collection/zoogenes) {% endhint %}
