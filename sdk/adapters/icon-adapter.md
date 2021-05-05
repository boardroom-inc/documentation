# Icon Adapter

A protocol integration can implement an adapter with the `IconAdapter` interface in order to provide a visual indicator for the protocol at various sizes.

## Interface

```typescript
interface Icon {
  size: string;
  url: string;
}

interface IconInfo {
  icons: Icon[];
}

export interface IconAdapter {
  getIcons: () => Promise<IconInfo>;
}
```

## Usage

To [query](../quick-start.md#querying-protocol-data) this information from the Governance SDK:

```typescript
const protocol = sdk.getProtocol(cname);

const icons = await protocol.adapter('icons').getIcons();

console.log(icons.map(icon => icon.url));
```

## Frameworks

The following pre-built adapters implement the `IconAdapter` interface:

* [CoinGecko](../governance-frameworks/coingecko.md)

