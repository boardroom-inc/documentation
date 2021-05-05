---
description: How to add support for a new protocol to the Governance SDK.
---

# Integrating Your Protocol

Support for a protocol can be added by submitting a pull request for a new protocol integration in the [Governance SDK monorepo](https://github.com/boardroom-inc/governance-sdk).

Protocols that use common governance frameworks or services will require very little code to integrate, but if a protocol does require some special mapping logic or has unique downstream data sources, completely custom protocol integrations can be authored.

## Protocol Registration

Protocols "register" with the SDK by implementing a `ProtocolRegistrationFunction` in the `gov-protocols` package of the SDK monorepo.

Protocol integrations are imperative functions that define some basic data for a protocol and register multiple adapter implementations that implement specific interfaces for querying governance data or enabling governance interactions.

Every protocol registration function _could_ potentially register multiple protocols at the same time -- this may make sense in some situations, but generally each protocol integration will have its own file. For instance, the Uniswap integration can be found at:

* `./packages/gov-protocols/src/uniswap.ts`

You can see all integration files here:

* [https://github.com/boardroom-inc/governance-sdk/tree/main/packages/gov-protocols/src](https://github.com/boardroom-inc/governance-sdk/tree/main/packages/gov-protocols/src)

### Example - Index Coop

Index Coop uses Snapshot for signed off-chain signaling of proposals, and is listed on CoinGecko. We can use the [prebuilt adapters](governance-frameworks/) to quickly integrate this protocol with the Governance SDK:

```typescript
import { ProtocolRegistrationFunction } from '@boardroom-labs/gov-lib';
import {
  CoinGeckoAdapter,
  SnapshotProposalsAdapter }
from '@boardroom-labs/gov-adapters';

export const register: ProtocolRegistrationFunction = (register, transports) => {
  register({
    cname: 'indexCoop',
    name: 'Index',
    adapters: (adapters) => {
      const snapshot = new SnapshotProposalsAdapter('index', transports);
      const coingecko = new CoinGeckoAdapter('index-cooperative', transports);
      adapters.implement('proposals', snapshot);
      adapters.implement('token', coingecko);
      adapters.implement('icons', coingecko);
    },
  });
};
```

* All registration functions should have a `ProtocolRegistrationFunction` type. This will correctly enforce return types and provide typings for the function parameters.
* The `register` function can be called multiple times to register multiple protocols in the same registration function, though unrelated protocols should still be implemented in separate modules.
* A protocol must, at minimum, specify the `cname` and `name` for that protocol. All other fields are optional
* Ensure that the `index.ts` file in `./packages/gov-protocols/src` is updated if a new integration file is added

