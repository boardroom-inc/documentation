# Vote Adapter

A protocol integration can implement an adapter with the `VoteAdapter` interface to allow a user to vote on a proposal.

## Interface

```typescript
export interface VoteAdapter {
  castVote: (proposalId: string, choice: number) => Promise<string>;
}
```

## Usage

Casting a vote requires a proposal ID \(resolved from a [Proposal Adapter](proposals-adapter.md)\) and the index of the proposal choice the user has selected. After submitting, an opaque request ID string will be returned that is implementation specific.

To submit a vote for a given proposal:

```typescript
const protocol = sdk.getProtocol(cname);

const requestId = await protocol.adapter('vote').castVote(proposalId, choice);

```

{% hint style="info" %}
You'll need a `signer` [transport](../transports.md) injected to the SDK for on-chain governance frameworks such as [Compound](../governance-frameworks/compound-governor-alpha.md).
{% endhint %}

## Frameworks

The following pre-built adapters implement the `VoteAdapter` interface:

* [Snapshot](../governance-frameworks/snapshot.md)
* [Compound Governor Alpha](../governance-frameworks/compound-governor-alpha.md)
* [Compound Governor Bravo](../governance-frameworks/compound-governor-bravo.md)
* [Aave Governance V2](../governance-frameworks/aave-governance-v2.md)

