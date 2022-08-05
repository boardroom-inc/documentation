# Snapshot

Snapshot is an off-chain signalling platform that uses signed payloads to create and vote on proposals. It provides a public API that can be used to query for proposal information.

{% hint style="info" %}
Check out Snapshot's "Hub API" here: [https://docs.snapshot.org/hub-api](https://docs.snapshot.org/hub-api)
{% endhint %}

## Using The Snapshot Adapter

As an example, Aavegotchi uses Snapshot for proposals: [https://snapshot.org/\#/aavegotchi.eth](https://snapshot.org/#/aavegotchi.eth)

You can see the Snapshot "space name" is `aavegotchi.eth` from URL above. The space name is all thats required to setup the Snapshot adapter:

```typescript
import { ProtocolRegistrationFunction } from '@boardroom/gov-lib';
import { SnapshotProposalsAdapter } from '@boardroom/gov-adapters';

export const register: ProtocolRegistrationFunction = (register, transports) => {
  register({
    cname: 'aavegotchi',
    name: 'Aavegotchi',
    adapters: (adapters) => {
      const snapshot = new SnapshotProposalsAdapter('aavegotchi.eth', transports);
      adapters.implement('proposals', snapshot);
      // ... other adapters
    },
  });
};

```

The snapshot adapter only implements the [Proposals Adapter](../adapters/proposals-adapter.md), so we announce a single adapter implementation to the SDK.

