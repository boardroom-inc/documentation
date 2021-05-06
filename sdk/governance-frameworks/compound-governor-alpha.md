# Compound Governor Alpha

Compound's Governor Alpha is a set of smart contracts that allow for on-chain snapshotting of token balances via a custom ERC-20 contract and on-chain submission, voting, and execution of proposals.

{% hint style="info" %}
You can view the Compound governance contracts their [@compound-finance/compound-protocol](https://www.coingecko.com/en/api) GitHub repo.
{% endhint %}

## Using the Compound Governor Alpha Adapter

As an example, Radical uses Compound's Governor Alpha contracts for their on-chain governance. The contract address is `0x690e775361AD66D1c4A25d89da9fCd639F5198eD`:

* [https://etherscan.io/address/0x690e775361AD66D1c4A25d89da9fCd639F5198eD](https://etherscan.io/address/0x690e775361AD66D1c4A25d89da9fCd639F5198eD)

The contract address is all we need to instantiate a `CompoundGovernorAlphaAdapter` instance:

```typescript
import { ProtocolRegistrationFunction } from '@boardroom/gov-lib';
import { CompoundGovernorAlphaAdapter } from '@boardroom/gov-adapters';

export const register: ProtocolRegistrationFunction = (register, transports) => {
  register({
    cname: 'radicle',
    name: 'Radicle',
    adapters: (adapters) => {
      const governor = new CompoundGovernorAlphaAdapter(
        '0x690e775361AD66D1c4A25d89da9fCd639F5198eD', transports);
      adapters.implement('proposals', governor);
      // ... other adapters
    },
  });
};
```

The Compound Governor Alpha adapter only implements the [Proposals Adapter](../adapters/proposals-adapter.md), so we announce a single adapter implementation to the SDK.

