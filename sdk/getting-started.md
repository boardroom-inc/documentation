---
description: Quick start guide for using the Governance SDK.
---

# Getting Started

## Installing the SDK

The Governance SDK is a NodeJS module that can be installed via npm or yarn:

```bash
npm i @boardroom-labs/gov-sdk
```

The Governance SDK will work both in server-side NodeJS environments as well as the Browser with a compilation tool like webpack or Babel.

{% hint style="info" %}
If you are wanting to build applications or experiences on top of read-only or aggregate governance data, or are not building for a NodeJS or browser environment, check out the [Boardroom API](../boardroom-api/boardroom-api.md) for integrating data sourced by the Governance SDK.
{% endhint %}

## Creating the SDK Instance

```typescript
import { GovSDK } from '@boardroom-labs/gov-sdk';

const sdk = new GovSDK();
```

The Governance SDK can be provided with transport-specific overrides to inject things like a custom JSON RPC provider for blockchain networks or a web3 provider / signer.

## Protocol Iteration and Introspection

Iterate through all supported protocols:

```typescript
for (const protocol of sdk.protocols()) {
  console.log(protocol.name);
}
```

Filter for only protocols that support a specific functionality \(implemented as "adapters"\):

```typescript
const protocols = [...sdk.protocols()];
const withTreasuryInfo = protocols.filter(p => p.hasAdapter('treasury'));
```

## Querying Protocol Data

All protocol interaction happens via "adapters", which are bound units of governance functionality that a protocol may implement:

```typescript
// this will throw if the protocol does not implement a TreasuryAdapter
const proposals = protocol.adapter('proposals');

// you can introspect the protocol to check if it implements
// a specific adapter first
if (protocol.hasAdapter('proposals')) {
  console.log(await protocol.adapter('proposals').getProposals({ limit: 5 }));
}
```

