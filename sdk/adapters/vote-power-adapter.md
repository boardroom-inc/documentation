# Vote Power Adapter

A protocol integration can implement an adapter with the `VotePower` interface to provide the current or historic vote power for a given batch of addresses.

## Interface

```typescript
export interface VotePowerInfo {
  address: string;
  power: number;
}

export interface VotePowerAdapter {
  getVotePower(addresses: string[], blockHeight?: number): Promise<VotePowerInfo[]>;	
}
```

## Usage

To resolve the vote power for an array of addresses at the current block:

```typescript
const protocol = sdk.getProtocol(cname);

const votePowers = await protocol.adapter('votePower').getVotePower(addresses);
```

## Frameworks

The following pre-built adapters implement the `VotePowerAdapter` interface:

* [Snapshot](../governance-frameworks/snapshot.md)
* [Compound Governor Alpha](../governance-frameworks/compound-governor-alpha.md)
* [Compound Governor Bravo](../governance-frameworks/compound-governor-bravo.md)
* [Aave Governance V2](../governance-frameworks/aave-governance-v2.md)

