# Aave Governance v2

Aave has their own on-chain governance architecture, collectively referred to as the **Aave Governance V2** contracts.

{% hint style="info" %}
You can view Aave's architecture and documentation on their [@aave/governance-v2](https://github.com/aave/governance-v2) GitHub repo.
{% endhint %}

## Using the Aave Governance V2 Adapter

Aave currently uses their Governance V2 for their protocol governance. The contract address is `0x690e775361AD66D1c4A25d89da9fCd639F5198eD`:

* [https://etherscan.io/address/0xEC568fffba86c094cf06b22134B23074DFE2252c](https://etherscan.io/address/0xEC568fffba86c094cf06b22134B23074DFE2252c)

The contract address is all we need to instantiate a `AaveGovernanceV2Adapter` instance:

```typescript
import { ProtocolRegistrationFunction } from '@boardroom/gov-lib';
import { AaveGovernanceV2Adapter } from '@boardroom/gov-adapters';

export const registerAave: ProtocolRegistrationFunction = (register, transports) => {
  register({
    cname: 'aave',
    name: 'Aave',
    adapters: (adapters) => {
      const coingecko = new CoinGeckoAdapter('aave', transports);
      const governance = new AaveGovernanceV2Adapter(
        '0xEC568fffba86c094cf06b22134B23074DFE2252c', transports);
      adapters.implement('proposals', governance);
      // ... other adapters
    },
  });
};
```

The Aave Governance V2 adapter only implements the [Proposals Adapter](../adapters/proposals-adapter.md), so we announce a single adapter implementation to the SDK.

