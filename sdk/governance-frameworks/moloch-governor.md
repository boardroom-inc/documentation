# Moloch Governor

Moloch Governor is a set of smart contracts that allow for a simple open-source DAO framework for grants-making.

{% hint style="info" %}
You can view the Moloch governance contracts on their [@MolochVentures/moloch](https://github.com/MolochVentures/moloch) GitHub repo.
{% endhint %}

## Using the Moloch Governor Adapter

As an example, TheLAO are currently using the contracts for their on-chain governance. The contract address is `0x8f56682a50becb1df2fb8136954f2062871bc7fc`:

* [https://etherscan.io/address/0x8f56682a50becb1df2fb8136954f2062871bc7fc](https://etherscan.io/address/0x8f56682a50becb1df2fb8136954f2062871bc7fc)

The contract address is all we need to instantiate a `MolochGovernorAdapter` instance:

```typescript
import { ProtocolRegistrationFunction } from '@boardroom/gov-lib';
import { CovalentAdapter, MolochGovernorAdapter } from '@boardroom/gov-adapters';

export const registerTheLAO: ProtocolRegistrationFunction = (register, transports) => {
  const cname = 'thelao';
  register({
    cname: cname,
    name: 'The LAO',
    category: ['Uncategorized'],

    adapters: (adapters) => {
      const governor = new MolochGovernorAdapter('0x8f56682a50becb1df2fb8136954f2062871bc7fc', transports, 1, cname);
      adapters.implement('proposals', governor);
      // ... other adapters
    },
  });
};
```

