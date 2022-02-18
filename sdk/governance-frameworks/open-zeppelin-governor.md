# Open Zeppelin Governor

This modular system of Governor contracts allows the deployment on-chain voting protocols similar to Compound’s Governor Alpha & Bravo and beyond, through the ability to easily customize multiple aspects of the protocol.

{% hint style="info" %}
You can view the Open Zeppelin governance contracts their [OpenZeppelin/openzeppelin-contracts](https://github.com/OpenZeppelin/openzeppelin-contracts/tree/master/contracts/governance) GitHub repo.
{% endhint %}

## Using the Open Zeppelin Adapter

As an example, ENS is currently using the Open Zeppelin contracts for their on-chain governance. The contract address is `0x323A76393544d5ecca80cd6ef2A560C6a395b7E3`:

* [https://etherscan.io/address/0x323A76393544d5ecca80cd6ef2A560C6a395b7E3](https://etherscan.io/address/0x323A76393544d5ecca80cd6ef2A560C6a395b7E3)

The contract address and token address is all we need to instantiate a `OpenZeppelinGovernorAdapter` instance:

```typescript
import { ProtocolRegistrationFunction } from '@boardroom/gov-lib';
import { OpenZeppelinGovernorAdapter } from '@boardroom/gov-adapters';

export const registerENS: ProtocolRegistrationFunction = (register, transports) => {
  const cname = 'ens';
  register({
    cname: cname,
    name: 'Ethereum Name Service',
    category: ['Protocol'],

    adapters: (adapters) => {
      const governor = new OpenZeppelinGovernorAdapter(
        '0x323A76393544d5ecca80cd6ef2A560C6a395b7E3',
        '0xC18360217D8F7Ab5e7c516566761Ea12Ce7F9D72',
        transports,
        cname
      );
      adapters.implement('createOnChainProposal', governor);
      adapters.implement('proposals', governor);
      adapters.implement('vote', governor);
      adapters.implement('delegation', governor);
      adapters.implement('votePower', governor);
      // ... other adapters
    },
  });
};
```

