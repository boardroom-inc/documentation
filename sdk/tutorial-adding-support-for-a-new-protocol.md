# Tutorial: adding support for a new protocol

## Step 1: Clone the `@boardroom-sdk` monorepo

At root level install dependencies with:

```bash
yarn
```

The monorepo uses lerna and yarn workspaces.

## Step 2: Add a new protocol folder

At root level, there is a folder called `protocol-package-example`, you can copy that folder into the `@boardroom-sdk/packages` and it already has proper configuration and structure to start development. Be sure to change the folder's name, to the protocol's name.

## Step 3: Declare the new protocol in the SDK's configuration file.

Open `@boardroom-sdk/packages/sdk/config.json` 

```javascript
{
  "protocols": ["compound", "yearn", "uniswap", "powerpool", "maker", "snapshot"]
}
```

And simply add the new protocol's name in the `protocols` array.

## Step 4: Build the @boardroom-sdk/base package

At root level, run:

```text
npm run build:base
```

This will build the base package that contains all common utilities and types so that they can be used in the development of the new protocol package.

## Step 5: Add a `schema` folder with the new protocol's `.graphql` schema types

Inside the `src/schema` folder, create a `.graphql` file for each entity of the new protocol's schema. If the types being created in the `.graphql` files have corresponding interfaces defined in the base package's schema, then the inheritance should be declared.

Declare types without namespacing.

For example, Compound has a `Proposal` type and there is also a `Proposal` interface:

```graphql
interface Proposal {
  id: ID!
  title: String
  description: String
  author: String
}
```

Then `packages/compound/src/schema/proposal.graphql` should look like this:

```graphql
type Proposal implements Proposal {
  forVotes: String!
  againstVotes: String!
  states: [ProposalState!]!
  proposer: DisplayCompAccount
  actions: [ProposalAction!]
}
```

These files should include a `query.graphql`.

```graphql
type Query {
  getProposals: [Proposal]
  getVoters: [Voter]
  getReceiptsResolver: [Receipt]
  getTokenHolders: [TokenHolder]
  getTokenHolder(id: String!): TokenHolder
}
```

Note in the example above, interface properties like `activeProtocols` are not declared in the `Voter` type. And the type name is `Voter` NOT `CompoundVoter`.

## Step 6: Define object mappers for each entity

Since the data directly returned from a protocol's API, subgraph or contracts has a different shape from the data returned by the SDK, mappers need to be defined so that raw data returned from the protocol's datasources gets transformed to match the defined GraphQL types from the previous steps.

Example:

`@boardroom-sdk/packages/compound/src/mappers.ts`

```typescript
export const proposalMapper = (p: any) => {
  return {
    __typename: 'CompoundProposal',
    id: p.id,
    title: p.title,
    description: p.description,
    againstVotes: p.against_votes,
    forVotes: p.for_votes,
    states: p.states.map(proposalStatesMapper),
    actions: p.actions? p.actions.map(proposalActionMapper): null,
    proposer: p.proposer? displayCompAccountMapper(p.proposer): null,
    author: p.proposer? p.proposer.id: null
  }
}
```

{% hint style="warning" %}
Note that optional fields, like `author` or `proposer` in this example, cannot be undefined; if they don't exist, then `null` must be returned.
{% endhint %}

## Step 7: Add the protocol's resolvers

In the resolvers file, declare each resolver function. If you'd like to learn more about implementing resolvers, read Apollo's full guide on implementing them: [https://www.apollographql.com/docs/apollo-server/data/resolvers/\#handling-arguments](https://www.apollographql.com/docs/apollo-server/data/resolvers/#handling-arguments).

Example:

`@boardroom-sdk/packages/compound/src/resolvers.ts`

```typescript
export const getProposalsResolver = async (root: any, args: any, context: any) => {
  const {
    proposals,
  } = await httpFetcher.get(COMPOUND_API_URL);

  const formattedProposals = proposals.map(proposalMapper)

  return formattedProposals
};
```

Certain resolvers are common for all protocols. Their signature is defined in `@boardroom/sdk/src/classes.ts`:

```typescript
export abstract class BoardroomProtocol {
  public client = new ApolloClient({
    cache: new InMemoryCache(),
    resolvers,
    typeDefs,
  })

  constructor(public ethereumApiUrl?: string, public config?: ProviderConfig) {}

  abstract getProposals(...args: any[]): Promise<Proposal[] | SnapshotProposal[]>
  abstract getVoters(...args: any[]): Promise<Voter[] | SnapshotVoter[]>
  abstract getVoteReceiptsByProposal(...args: any[]): Promise<VoteReceipt[] | SnapshotPollVote[]>
  abstract getVoteReceiptsByVoter(...args: any[]): Promise<VoteReceipt[] | SnapshotHarvesterVoteReceipt[]>
  abstract getGovernanceData(...args: any[]): Promise<Governance | SnapshotGovernance>
}

export abstract class OnChainProtocol extends BoardroomProtocol {
  abstract getProposals(fetchOptions?: FetchOptions): Promise<Proposal[]>
  abstract getVoters(fetchOptions?: FetchOptions): Promise<Voter[]>
  abstract getVoteReceiptsByProposal(proposalId: string, fetchOptions?: FetchOptions): Promise<VoteReceipt[]>
  abstract getVoteReceiptsByVoter(voterAddress: string, fetchOptions?: FetchOptions): Promise<VoteReceipt[]>
  abstract getGovernanceData(): Promise<Governance>
}

```

#### When implementing one of these resolvers, the name and signature should match its definition exactly.

{% hint style="danger" %}
If the new protocol that you are adding support for, contains one of the methods above and the signature in the protocol specific package does not match the one above, the `@boardroom/sdk` build will fail
{% endhint %}

{% hint style="info" %}
All OnChain protocols are abstracted under the `OnChainProtocol` abstract class
{% endhint %}

## Step 8: Export TypeDefs and Resolvers

Export the resolvers from `resolvers.ts` like so:

```typescript
export const resolvers = {
  Query: {
    getProposals: getProposalResolver,
    getVoters: getVotersResolver,
    getReceipts: getReceiptsResolver,
    getTokenHolders: getTokenHoldersResolver,
    getTokenHolder: getTokenHolderResolver
  }
}
```

Note that all the `resolvers` in the `Query` object should match the `.graphql` Query type fields 1:1. For example, for the resolvers above, the `query.graphql` file looks like this:

`@boardroom-sdk/packages/compound/src/schema/query.graphql`

```graphql
type Query {
  getProposals: [Proposal]
  getVoters: [Voter]
  getReceipts: [Receipt]
  getTokenHolders: [TokenHolder]
  getTokenHolder(id: String!): TokenHolder
}
```

Copying the same `index.ts` that the other packages use in the `src` folder of your package is sufficient.

## Step 9: Add filtering and sorting to queries

Currently, filtering and sorting are performed on the client side; this means that a query to a datasource is executed \(a subgraph query, for example\) and after receiving the results the filters are applied.

This implies that filtering and sorting DO NOT impact performance. But pagination alters the amount of results fetched from each datasource, so pagination arguments DO impact performance.

To add filters/sorting to a query, simply declare a `fetchOptions` argument of type `String` in the query schema definition file:

```graphql
type Query {
  getProposals(fetchOptions: String): [Proposal]
  getVoters(fetchOptions: String): [Voter]
  getReceipts(fetchOptions: String): [Receipt]
  getTokenHolders(fetchOptions: String): [TokenHolder]
  getTokenHolder(id: String!): TokenHolder
}
```

Then, wrap the queries that will support filtering with the `addFilter` and `addSorting`functions from the base package.

```typescript
import { addFilter } @boardroom-sdk/base

export const resolvers = {
  Query: {
    getProposals: addSorting(addFilter(getProposalResolver)),
    getVoters: addSorting(addFilter(getVotersResolver)),
    getReceipts: addSorting(addFilter(getReceiptsResolver)),
    getTokenHolders: addSorting(addFilter(getTokenHoldersResolver)),
    getTokenHolder: addSorting(addFilter(getTokenHolderResolver))
  }
}
```

Additionally, you can define your own addFilter or addSorting function with your own custom filtering/sorting logic.

{% hint style="danger" %}
Adding `addSorting` or `addFilter` to a query that does not return an array will result in a build error when building the @boardroom/sdk package
{% endhint %}

## Step 10: Add pagination to queries

Pagination is added differently from sorting and filtering. Since pagination alters the request being sent to the datasource, and many different datasources are used in the SDK, it has to be implemented manually for each case. In some cases, pagination is not possible since the datasource does not support it \(like Snapshot\). However, subgraphs, which are widely used for OnChain governance data fetching supports pagination with the same syntax.  
  
An example would be:

```typescript
import { GraphqlFetcher, getPaginationArgsForSubgraph } from '@boardroom/base'

export const getProposalsResolver = async (_: any, args: any, context: any) => {
  const { first, skip } = getPaginationArgsForSubgraph(args, 100)
  
  const query = gql`
    {
      proposals(first: ${first}, skip: ${skip}, orderBy: id, orderDirection: desc) {
        id
        proposer {
          id
        }
        startBlock
        endBlock
        description
        status
        targets
        calldatas
        values
        executionETA
        votes {
          id
        }
      }
    }
  `;
  const { proposals } = await graphQLFetcher.query(query)
```

Note that `getPaginationArgsForSubgraph` is an utility function imported from the base package that automatically parses the resolver's `args` parameter and transforms its `paginate` object \(if it exists\) into a subgraph's `first`and `skip` arguments. These are embedded in the subgraph query as shown above and pagination is performed. `getPaginationArgsForSubgraph`'s second argument is a number which indicates the default page size. This argument exists because different objects may have different default page sizes based on their size \(proposals's default page size should be lower than vote receipts's page size\)

However, other protocols, like Compound have their own API which supports their own pagination arguments. Therefore, implementation should adapt accordingly, as stated before, in a per-case basis.

Pagination for Compound:

```typescript
const addPaginationToUrl = (url: string, args: any) => {
  if(args) {
    const fetchOptions = args.fetchOptions && JSON.parse(args.fetchOptions)
    const paginate = fetchOptions && fetchOptions.paginate

    const page = paginate?.page;
    const pageSize = paginate?.pageSize;

    return `${url}?page_size=${pageSize || 200}&page_number=${page || 1}`;
  }

  return url;
};

export const getProposalsResolver = async (_: any, args: any) => {
  const { proposals } = await httpFetcher.get(
    addPaginationToUrl("proposals", args)
  );
}
```

## Step 10: Run protocol packages code generation

Navigate to the monorepo's root level.

Then open a terminal and:

```bash
yarn codegen:packages
```

This should generate in the `@boardroom-sdk/packages/your-new-protocol/src` folder, a new `generated` folder that contains a bundled schema.graphql file, a typescript types file that matches the bundled schema definitions, namespaced resolvers already properly mapped, and autogenerated GraphQL queries already properly annotated.

## Step 11: Add tests for your new protocol package

The Boardroom SDK makes use of `apollo-boost` and `apollo-link-state` for runtime data validation and sanitization. 

Because of the SDK's code generation, type definition changes don't require manual interface maintenance. 

Schema type changes won't change the tests, if the actual data returned by a resolver does not match the proper type definition declared in GraphQL, Apollo Client will throw a warning and won't return data.

```typescript
import ApolloClient, { gql } from 'apollo-boost'
import protocol from '../src'
import { getCompoundProposals } from '../src/generated/operations/annotatedQueries'
import nodeFetch from 'node-fetch'

jest.setTimeout(60000)

const client = new ApolloClient({
  fetch: nodeFetch as any,
  resolvers: protocol.namespacedResolvers,
  typeDefs: protocol.typeDefs,
})

describe("Compound Resolvers", () => {
  it("GetProposals works", async () => {
    const { data } = await client.query({ query: gql`${getCompoundProposals}` })

    expect(data).not.toBeNull()
    expect(data.getCompoundProposals).toBeDefined()
    expect(Array.isArray(data.getCompoundProposals)).toEqual(true)
  })
})
```

If `proposalMapper` defined in a previous step, is missing a field, like `description` for example, Apollo will throw a semantic error similar to this one:

```text
console.warn
    Missing field description in {
      "__typename": "CompoundProposal",
      "id": 9,
      "title": "Set reserve factor for cUSDT to 20.0%",

      at Function.warn (../../node_modules/ts-invariant/lib/invariant.esm.js:29:32)
      at ../../node_modules/apollo-cache-inmemory/lib/bundle.cjs.js:782:77
          at Array.forEach (<anonymous>)
      at StoreWriter.writeSelectionSetToStore (../../node_modules/apollo-cache-inmemory/lib/bundle.cjs.js:750:29)
      at ../../node_modules/apollo-cache-inmemory/lib/bundle.cjs.js:938:15
          at Array.map (<anonymous>)
      at StoreWriter.processArrayValue (../../node_modules/apollo-cache-inmemory/lib/bundle.cjs.js:915:18)

```

Then, you would modify `proposalMapper` to include `description` field and run the tests again.

{% hint style="info" %}
Mappers or resolvers files changes do not require re-running code generation or package building to re-test.
{% endhint %}

## Step 12: Run SDK code generation

At root level run 

```text
yarn build
```

This should generate in the `@boardroom-sdk/sdk` package the appropriate Typescript types and interfaces based on the protocol's schema, aggregate the newly created resolvers to the rest, generate a new protocol class where each method represents a query/mutation, everything namespaced properly and typesafe.

