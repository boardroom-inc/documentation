# Compound Governor Bravo

Compound's Governor Bravo is a set of smart contracts that allow for on-chain snapshotting of token balances via a custom ERC-20 contract and on-chain submission, voting, and execution of proposals.

{% hint style="info" %}
You can view the Compound governance contracts their [@compound-finance/compound-protocol](https://www.coingecko.com/en/api) GitHub repo.
{% endhint %}

## Changes from Governor Alpha

The following are the relevant changes between Compound Alpha and Bravo governor contract:

* **Abstaining on votes**. Voters can chose a third option, `ABSTAIN`, when voting on a proposal. This means all proposals read from a protocol with Governor Bravo contracts will have _three_ options instead of the usual two.

{% hint style="info" %}
To see a complete discussion of changes, see [Governor Bravo Development](https://www.comp.xyz/t/governor-bravo-development/942) on the Compound forums.
{% endhint %}

## Using the Compound Governor Bravo Adapter

As an example, Compound themselves are currently using the Governor Bravo contracts for their on-chain governance. The contract address is `0x690e775361AD66D1c4A25d89da9fCd639F5198eD`:

* [https://etherscan.io/address/0xc0Da02939E1441F497fd74F78cE7Decb17B66529](https://etherscan.io/address/0xc0Da02939E1441F497fd74F78cE7Decb17B66529)

The contract address is all we need to instantiate a `CompoundGovernorBravoAdapter` instance:

```typescript
import { ProtocolRegistrationFunction } from '@boardroom/gov-lib';
import { CompoundGovernorBravoAdapter } from '@boardroom/gov-adapters';

export const register: ProtocolRegistrationFunction = (register, transports) => {
  register({
    cname: 'compound',
    name: 'Compound',
    adapters: (adapters) => {
      const governor = new CompoundGovernorBravoAdapter(
        '0xc0Da02939E1441F497fd74F78cE7Decb17B66529', transports);
      adapters.implement('proposals', governor);
      // ... other adapters
    },
  });
};
```

The Compound Governor Bravo adapter only implements the [Proposals Adapter](../adapters/proposals-adapter.md), so we announce a single adapter implementation to the SDK.

