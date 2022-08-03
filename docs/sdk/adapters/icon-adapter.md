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

To [query](../governance-sdk/quick-start.md#querying-protocol-data) this information from the Governance SDK:

```typescript
const protocol = sdk.getProtocol(cname);

const icons = await protocol.adapter('icons').getIcons();

console.log(icons.map(icon => icon.url));
```

## Frameworks

The following pre-built adapters implement the `IconAdapter` interface:

* [CoinGecko](../governance-frameworks/coingecko.md)

## Integration

If you are integration your protocol with the Governance SDK, you can chose to instead hard-code your icons if you'd rather manually provide them and not use an existing pre-built adapter:

```typescript
import { IconAdapter, IconInfo } from '@boardroom/gov-lib';

export class HardcodedIconAdapter implements IconAdapter {

  // function still needs to be async to implement the correct
  // interface, but we can just hard-code values if needed
  async getIcons(): Promise<IconInfo> {
    return {
      icons: [
        { name: 'default', url: 'https://cdn.mysite.com/icon.png' }
      ]
    }
  }
  
}
```
