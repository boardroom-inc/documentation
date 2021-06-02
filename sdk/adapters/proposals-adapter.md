# Proposals Adapter

A protocol integration can implement an adapter with the `ProposalsAdapter` interface to provide information about governance proposals and submitted votes

## Interface

```typescript
export interface PaginationOptions {
  cursor?: string;
}

export interface ExternalLink {
  url: string;
  name: string;
}

export type Time = { timestamp: number } | { blockNumber: number };

export interface Proposal {
  id: string;
  title: string;
  proposer: string;
  externalUrl?: string;
  content: string;
  choices: string[];
  blockNumber: number;
  startTime: Time;
  endTime: Time;
}

export interface Vote {
  time: Time;
  proposalId: string;
  address: string;
  choice: number;
  power: number;
  reason?: string;
}

export interface ProposalEvent {
  event: 'queued' | 'canceled' | 'executed';
  time: Time;
}

export interface ProposalPage {
  items: Proposal[];
  nextCursor?: string;
}

export interface VotePage {
  items: Vote[];
  nextCursor?: string;
}

export interface ProposalEventPage {
  items: ProposalEvent[];
  nextCursor?: string;
}

export interface ProposalsAdapter {
  getProposals: (pagination?: PaginationOptions) => Promise<ProposalPage>;
  getProposalEvents: (pagination?: PaginationOptions) => Promise<ProposalEventPage>;
  getVotes: (pagination?: PaginationOptions) => Promise<VotePage>;
  getExternalLink: () => Promise<ExternalLink>;
}
```

## Usage

To [query](../quick-start.md#querying-protocol-data) this information from the Governance SDK:

```typescript
const protocol = sdk.getProtocol(cname);

// fetch the first page of proposals
const proposals = await protocol.adapter('proposals').getProposals();

// fetch a page of proposals starting from a specific cursor
const proposals = await protocol.adapter('proposals').getProposals({ cursor });

// get the first page of votes across all protocols
const votes = await protocol.adapter('proposals').getVotes();
```

### Pagination

The `getProposals` and `getVotes` methods are both paginated. Not all [pre-built adapters](../governance-frameworks/) actually implement pagination as it may not be possible with the downstream data source, but pagination options can always be passed in to the adapters safely.

You can use some of the built-in utilities to stream or buffer any paginated methods in the SDK:

```typescript
import { bufferAsyncIterable, iteratePaginatedResponse } from '@boardroom/gov-sdk';

// create an async iterator that will iterate through all items across all pages
const proposals = iteratePaginatedResponse(
  (cursor) => protocol.adapter('proposals', instance).getProposals({ cursor }));

// stream all proposals for further processing
for await (const proposal of proposals) {
  // ... further processing
}

// or buffer all items into an array
const allProposals = await bufferAsyncIterable(proposals);
```

## Frameworks

The following pre-built adapters implement the `ProposalsAdapter` interface:

* [Snapshot](../governance-frameworks/snapshot.md)
* [Compound Governor Alpha](../governance-frameworks/compound-governor-alpha.md)
* [Compound Governor Bravo](../governance-frameworks/compound-governor-bravo.md)
* [Aave Governance V2](../governance-frameworks/aave-governance-v2.md)

## Integration

If a protocol integration is using an existing governance framework like Compound or Aave, but also has a custom UI / governance dApp, the `getExternalLink` method can be overridden:

```typescript
class CompoundProposalAdapter extends CompoundGovernorBravoAdapter {
  async getExternalLink(): Promise<ExternalLink> {
    return {
      name: 'Compound Governance',
      url: 'https://compound.finance/governance',
    };
  }
}

export const register: ProtocolRegistrationFunction = (register, transports) => {
  register({
    cname: 'compound',
    name: 'Compound',
    adapters: (adapters) => {
      const governor = new CompoundProposalAdapter(
        '0xc0Da02939E1441F497fd74F78cE7Decb17B66529', transports);
      adapters.implement('proposals', governor);
      // ... other adapters ...
    },
  });
};
```

Adapters will implement a default behavior for this, for on-chain governance contracts it will simply surface an Etherscan link if not customized like the above snippet.

