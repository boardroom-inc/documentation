# Delegation Adapter

A protocol integration can implement an adapter with the `DelegationAdapter` interface to allow a user to delegate their voting power to another address .

## Interface

```typescript
export interface DelegationAdapter {
  delegateVotingPower: (address: string) => Promise<string>;
}
```

## Usage

To delegate vote power to a specific address:

```typescript
const protocol = sdk.getProtocol(cname);

const requestId = await protocol.adapter('delegation')
  .delegateVotingPower(delegateAddress);

```

After submitting, an opaque request ID string will be returned that is implementation specific.

{% hint style="info" %}
You'll need a `signer` [transport](../transports.md) injected to the SDK for all delegation frameworks.
{% endhint %}

## Frameworks

The following pre-built adapters implement the `DelegationAdapter` interface:

* [Compound Governor Alpha](../governance-frameworks/compound-governor-alpha.md)
* [Compound Governor Bravo](../governance-frameworks/compound-governor-bravo.md)
* [Aave Governance V2](../governance-frameworks/aave-governance-v2.md)

