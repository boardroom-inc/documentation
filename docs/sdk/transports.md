# Transports

Transports are the low-level connection implementations that allow the Governance SDK to interact with external data sources.

To ensure maximum flexibility, SDK consumers can [inject](https://en.wikipedia.org/wiki/Dependency_injection) transport instances when creating an SDK instance, allowing any custom behavior or overrides of how downstream dependencies like blockchain nodes or HTTP endpoints are handled.

## Injecting Transports

When instantiating an instance of the SDK, you _may_ provide several transport instances. The SDK will only attempt to resolve a transport instance when a method is called that requires that specific transport.

{% hint style="info" %}
You don't need to provide all transports if you do not anticipate using any functionality that is dependent on it. For example, if you do not need to execute any mutations, you don't need to provide a `signer` transport.
{% endhint %}

The following transports are used in the Governance SDK:

* `ipfs` - Resolves files from the IPFS network. If not provided, a default implementation is used.
* `http` - Makes basic HTTP requests. If not provided, a default implementation is used.
*  `rpc` - Resolves a standard `JsonRpcProvider` instance on a per-network basis.
* `signer` - Used to sign payloads and provide a standard `JsonRpcSigner` instance.

### Example

Instantiating the Governance SDK with a few different JSON RPC providers:

```typescript
import { GovernanceSDK, NetworkTransportResolver } from '@boardroom/gov-sdk';
import { JsonRpcProvider } from '@ethersproject/providers';
 
 const sdk = new GovernanceSDK({
    transports: {
      
      rpc: new NetworkTransportResolver({
        1: new JsonRpcProvider(ETH_RPC_NODE),
        137: new JsonRpcProvider(POLYGON_RPC_NODE, 137),
        // ... additional chains
      }),
      
      http: 
    },
  });
```

Using SDK within a React Hook and injecting a signer instance:

```typescript
import { GovernanceSDK, SignerTransport } from '@boardroom/gov-sdk';
import { useEthers } from '@usedapp/core';

export const useGovernanceSDK = () => {
  const { library } = useEthers();
  const signer = library?.getSigner();

  const sdk = new GovernanceSDK({
    transports: {
      // ...
      signer: new SignerTransport(signer),
    },
  });
  
  // ...
  
};
```

