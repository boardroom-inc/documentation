# Token Adapter

A protocol integration can implement an adapter with the `TokenAdapter` interface in order to surface basic token information and market stats for the protocol.

## Interface

```typescript
interface CurrencyAmount {
  currency: string;
  amount: string;
}

interface ContractAddress {
  network: string;
  address: string;
}

interface TokenInfo {
  symbol: string;
  contractAddress: ContractAddress;
  currentMarketPrice: CurrencyAmount;
}

export interface TokenAdapter {
  getInfo: (currency?: Currency, network?: Network) => Promise<TokenInfo>;
}
```

## Usage

To [query](../governance-sdk/quick-start.md#querying-protocol-data) this information from the Governance SDK:

```typescript
const protocol = sdk.getProtocol(cname);

const info = await protocol.adapter('token').getInfo();

console.log(info.currentMarketPrice);
```

## Frameworks

The following pre-built adapters implement the `TokenAdapter` interface:

* [CoinGecko](../governance-frameworks/coingecko.md)
* [Uniswap V2](../governance-frameworks/uniswap-v2.md)
