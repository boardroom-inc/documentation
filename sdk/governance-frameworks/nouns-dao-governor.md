# Nouns DAO Governor

Nouns Governor is a set of smart contracts that allow for on-chain snapshotting of token balances via a custom ERC-721 contract and on-chain submission, voting, and execution of proposals.

You can view the Nouns governance contracts on their [@nounsDAO/nouns-monorepo](https://github.com/nounsDAO/nouns-monorepo/tree/master/packages/nouns-contracts/contracts/governance) GitHub repo.

### Using the Nouns DAO Governor Adapter

As an example, Nouns themselves are currently using the contracts for their on-chain governance. The contract address is `0x6f3E6272A167e8AcCb32072d08E0957F9c79223d`:

* [https://etherscan.io/address/0x6f3E6272A167e8AcCb32072d08E0957F9c79223d](https://etherscan.io/address/0x6f3E6272A167e8AcCb32072d08E0957F9c79223d)

The contract address along with the token address is all we need to instantiate a `NounsGovernorAdapter` instance:

```
import { ProtocolRegistrationFunction } from '@boardroom/gov-lib';
import { NounsGovernorAdapter } from '@boardroom/gov-adapters';

export const register: ProtocolRegistrationFunction = (register, transports) => {
  register({
    cname: 'nounsdao',
    name: 'Nouns DAO',
    adapters: (adapters) => {
      const governance = new NounsGovernorAdapter(
        '0x6f3E6272A167e8AcCb32072d08E0957F9c79223d',
        '0x9C8fF314C9Bc7F6e59A9d9225Fb22946427eDC03',
        transports
      );

      adapters.implement('proposals', governance);
      // ... other adapters
    },
  });
};
```
