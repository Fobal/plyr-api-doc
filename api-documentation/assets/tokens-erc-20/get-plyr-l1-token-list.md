---
description: Get list of available PLYR L1 tokens and their details including prices and metadata
---

# Get PLYR L1 Token List

{% hint style="info" %} Retrieve the list of available PLYR L1 tokens with detailed information including prices, metadata, and chain information. {% endhint %}

**Endpoint:** `/tokenlist`  
**Method:** GET

{% tabs %} {% tab title="Success Response (200)" %}

```typescript
{
    name: string,
    timestamp: string,
    version: {
      major: number,
      minor: number,
      patch: number
    },
    tokens: Array<{
      chainId: number,
      address: string,
      name: string,
      symbol: string,
      decimals: number,
      logoURI: string,
      apiId: string,
      cmcURL: string,
      cmcId: string,
      cgURL: string,
      cgId: string,
      website: string,
      category: string,
      shortDescription: string,
      nativeChainId: number,
      nativeChainName: string,
      nativeChainLogoURI: string,
      nativeContractAddress: string,
      isGameStake: boolean,
      price: number,
      updatedAt: string,
      nextUpdatedAt: string
    }>
 }
```

{% endtab %}

{% tab title="Error Response (404)" %}

```typescript
{
  error: "Failed to retrieve token list",
}
```

{% endtab %} {% endtabs %}

### Response Fields Description

-   `name`: Name of the token list
-   `timestamp`: Last update timestamp
-   `version`: Semantic version of the token list
-   `tokens`: Array of token objects with the following properties:
    -   `chainId`: ID of the blockchain network
    -   `address`: Token contract address
    -   `name`: Token name
    -   `symbol`: Token symbol
    -   `decimals`: Number of decimal places
    -   `logoURI`: URL to token's logo image
    -   `apiId`: Unique identifier for the token in the API
    -   `cmcURL`: CoinMarketCap URL
    -   `cmcId`: CoinMarketCap ID
    -   `cgURL`: CoinGecko URL
    -   `cgId`: CoinGecko ID
    -   `website`: Official token website
    -   `category`: Token category
    -   `shortDescription`: Brief description of the token
    -   `nativeChainId`: ID of the token's native blockchain
    -   `nativeChainName`: Name of the token's native blockchain
    -   `nativeChainLogoURI`: URL to native chain's logo
    -   `nativeContractAddress`: Token's contract address on its native chain
    -   `isGameStake`: Whether the token can be used for game staking
    -   `price`: Current token price in USD
    -   `updatedAt`: Last price update timestamp
    -   `nextUpdatedAt`: Next scheduled price update timestamp
