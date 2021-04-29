---
description: How to add support for a new protocol to the Governance SDK.
---

# Integrating Your Protocol

Support for a protocol can be added by submitting a pull request for a new protocol integration in the Boardroom SDK.  

Protocols that use common governance frameworks or services will require very little code to integrate, but if a protocol does require some special mapping logic or has unique downstream datasources, completely custom protocol integrations can be authored.

## Protocol Registration

Protocols "register" with the SDK by implementing a `ProtocolRegistrationFunction` in the `gov-protocols` package of the SDK monorepo.

Protocol integrations are imperative functions that define some basic data for a protocol and register multiple adapter implementations that implement specific interfaces for querying governance data or enabling governance interactions.

### Example - Index Coop

Index Coop uses Snapshot for signed off-chain signalling of proposals, and is listed on CoinGecko. We can use the [prebuilt adapters](governance-frameworks/) to quickly integrate this protocol with the Governance SDK:

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



