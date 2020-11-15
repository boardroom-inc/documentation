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

## Step 9: Add filters to queries

To add filters to a query, simply declare a `filter` argument of type `String` in the query schema definition file:

```graphql
type Query {
  getProposals(filter: String): [Proposal]
  getVoters(filter: String): [Voter]
  getReceipts(filter: String): [Receipt]
  getTokenHolders(filter: String): [TokenHolder]
  getTokenHolder(id: String!): TokenHolder
}
```

Then, wrap the queries that will support filtering with the `addFilter` function from the base package.

```typescript
import { addFilter } @boardroom-sdk/base

export const resolvers = {
  Query: {
    getProposals: addFilter(getProposalResolver),
    getVoters: addFilter(getVotersResolver),
    getReceipts: addFilter(getReceiptsResolver),
    getTokenHolders: addFilter(getTokenHoldersResolver),
    getTokenHolder: addFilter(getTokenHolderResolver)
  }
}
```

Additionally, you can define your own addFilter function with your own custom filtering logic

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

## Step 12: Run SDK code generation

At root level run 

```text
yarn build
```

This should generate in the `@boardroom-sdk/sdk` package the appropriate Typescript types and interfaces based on the protocol's schema, aggregate the newly created resolvers to the rest, generate a new protocol class where each method represents a query/mutation, everything namespaced properly and typesafe.

