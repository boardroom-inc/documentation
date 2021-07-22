---
description: Simple getting started guide for using the Governance SDK.
---

# SDK Quick Start

## Installing the SDK

The Governance SDK is a NodeJS module \(with native TypeScript types\) that can be installed via npm or yarn:

```bash
npm i @boardroom/gov-sdk
```

The Governance SDK will work both in server-side NodeJS environments as well as the Browser with a compilation tool like webpack or Babel.

{% hint style="info" %}
If you are wanting to build applications or experiences on top of read-only or aggregate governance data, or are not building for a NodeJS or browser environment, check out the [Boardroom API](../boardroom-api/boardroom-api.md) for quickly integrating data sourced by the Governance SDK.
{% endhint %}

## Creating the SDK Instance

```typescript
import { GovernanceSDK } from '@boardroom/gov-sdk';

const sdk = new GovernanceSDK();
```

The Governance SDK can be provided with transport-specific overrides to inject things like a custom JSON RPC provider for blockchain networks or a web3 provider / signer.

### Injecting Transports

You will want to generally _at least_ provide an Ethereum RPC provider instance, as that powers most read-only operations such as computing snapshot voting power or reading from on-chain governance contracts. 

As an example, you can use Ethers' `JsonRpcProvider` implementation and point it to a HTTP RPC node from a provider like Infura or Alchemy:

```typescript
import { GovernanceSDK, NetworkTransportResolver } from '@boardroom/gov-sdk';
import { JsonRpcProvider } from '@ethersproject/providers';

// ...

const rpc = new NetworkTransportResolver({
  1: new JsonRpcProvider(ETH_RPC_NODE)
});

const sdk = new GovernanceSDK({ transports: { rpc } });
```

{% page-ref page="transports.md" %}

## Protocol Iteration and Introspection

The `GovernanceSDK` instance is primarily used to get access to `Protocol` instances. Protocols are surfaced as normalized objects that are composed of various [Adapter](adapters/) implementations.

Iterate through all supported protocols:

```typescript
for (const protocol of sdk.getAllProtocols()) {
  console.log(protocol.name);
}
```

Filter for only protocols that support a specific functionality:

```typescript
const protocols = sdk.getAllProtocols();
const withTreasuryInfo = protocols.filter(p => p.hasAdapter('treasury'));
```

You can directly get a protocol by it's **cname**, which is an arbitrary string identifier used to reference a protocol:

```typescript
// this will throw if "aave" is not registered with the SDK
const aave = sdk.getProtocol('aave');

const info = await aave.adapter('token').getInfo('usd');
```

## Querying Protocol Data

All protocol interaction happens via [Adapters](adapters/), which are bound units of governance functionality that a protocol may implement:

```typescript
// this will throw if the protocol does not implement a TreasuryAdapter
const proposals = protocol.adapter('proposals');

// you can introspect the protocol to check if it implements
// a specific adapter first
if (protocol.hasAdapter('proposals')) {
  console.log(await protocol.adapter('proposals').getProposals({ limit: 5 }));
}
```

{% hint style="info" %}
**Using the Governance SDK directly means your code will be directly invoking downstream data sources,** such as reading from the Snapshot API, or querying the blockchain over an RPC node.
{% endhint %}

