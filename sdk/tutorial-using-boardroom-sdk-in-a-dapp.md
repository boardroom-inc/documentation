---
description: >-
  How to integrate Boardroom SDK into your web application to read and write
  data from governance protocols.
---

# Tutorial: using Boardroom SDK in a dApp

## Step 1: Query data from a specific protocol

For this example we will use `Compound` protocol.

```typescript
import { Compound, CompoundProposal } from '@boardroom-sdk/sdk';

const getCompoundProposals: Promise<CompoundProposal[]> = async () => {
  const compound = new Compound()
  const proposals = await compound.getProposals()

  return proposals
}
```

In the example above, we are importing the `Compound` class, we declare our function's return type with the imported type `CompoundProposal`. Then we instantiate the protocol object and call the `getProposals` method with a filter object to retrieve all Compound proposals that are open at the moment.

Some methods require the user to pass certain arguments in order to perform the read/write operation. This is done by simply passing the required parameters, Typescript's compiler will complain if a required argument isn't passed, since all classes, methods and data is typesafe.

```typescript
import { Snapshot } from '@boardroom-sdk/sdk';

const snapshot = new Snapshot()

const yearnVoters = await snapshot.getVoters('yearn', 'QmVzvqJwnnEhnJGxDoKZNNkeRXvrmscrhwpLbZrQxw1mkf')
```

## Step 2: Query data from different protocols

```typescript
import { Base, Proposal } from '@boardroom-sdk/sdk';

const getCompoundProposals: Promise<Proposal[]> = async () => {
  const base = new Base()
  const proposalsByProtocol = await base.getProposals()

  const proposals = Object.values(proposalsByProtocol).flat()

  const { Compound: compoundProposals } = proposalsByProtocol

  return proposals
}
```

In this example, we are getting open proposals across all protocols and then we are taking Compound proposals only, by destructuring the `proposalsByProtocol` object.

## Step 3: Filtering and paginating data

```typescript
  // Defaults to page 1, pageSize 2000 and no filter
  const aProposals = await compound.getProposals()

  // Defaults to page 1, pageSize 2000 and filter by Id, so this will only yield 1 proposal
  const bProposals = await compound.getProposals(
    null, null, { where: { id: '1' }}
  )

  // Defaults to page 1, pageSize 50 and no filter  
  const cProposals = await compound.getProposals(
    null, 50
  )

  // Defaults to page 2, pageSize 2000 and no filter
  const dProposals = await compound.getProposals(2)

  // Page 2, pageSize 100 and filter by no votes against
  const eProposals = await compound.getProposals(
    2, 100, { where: { againstVotes: '0' }}
  )
  
  // Defaults to page 1, pageSize 2000
  // Query for Compound proposals with againstVotes === '0' AND author === null
  const fProposals = await compound.getProposals(null, null, { where: {
    againstVotes: '0',
    author: null
  }, conditionType: 'AND' })
  
  // Defaults to page 1, pageSize 2000
  // Query for Compound proposals with againstVotes === '0' OR author === null
  const gProposals = await compound.getProposals(null, null, { where: {
    againstVotes: '0',
    author: null
  }, conditionType: 'OR' })
```

Currently, Boardroom SDK supports basic data filtering, by passing a filter argument.  It contains a `where` object that holds the properties and values the returned entities should match, and a `conditionType` boolean that can be either `'OR'` or `'AND'` \(if undefined, will default to `'AND'`\).

If `conditionType` is `'AND'`, then the returned entities must match all properties and values in the `where` object. If`'OR'` then it needs to match only one of them.

{% hint style="info" %}
Not all queries support pagination. If the query you are invoking support pagination, typesafety will indicate it.
{% endhint %}

## Querying through an Apollo Client

In case you wish to implement your own classes, writing your own queries and mutations, you can do so by importing aggregated resolvers and type definitions to instantiate an `ApolloClient`:

```typescript
import { ApolloClient, gql, InMemoryCache } from 'apollo-boost'
import { resolvers, typeDefs } from '@boardroom-sdk/sdk'

const apolloClient = new ApolloClient({
  cache: new InMemoryCache(),
  resolvers,
  typeDefs
})

const query = gql`
  query {
    getCompoundProposals @client {
      id
    }
  }
`

const { data: { getCompoundProposals: cProposals } } = await apolloClient.query({ query })
```

Some queries require certain arguments to be passed in order for their resolvers to fetch the correct data:

```typescript
const query = gql`
  query {
    getMakerSpellData(spellAddress: $spellAddress ) @client {
      eta
      datePassed
    }
  }
`

const { data: { getMakerSpellData } } = await apolloClient.query({ 
  query, variables: {spellAddress: '0x96f6cd23fd450d30a12ea0d14fcecc8ae8b4bc25'}
})
```

{% hint style="warning" %}
**Note**: user's custom queries must be annotated with Apollo's `@client` annotation, as shown in the examples above.
{% endhint %}

## Querying through an Apollo Client, using a protocol specific package

Instead of using the aggregated resolvers and type definitions, you can simply use only a protocol's resolvers and type definitions.

To do this, install the protocol package you wish to use:

```bash
npm i --save @boardroom-sdk/yearn
```

Then, resolvers \(namespaced or not\) and typedefs can also be imported directly:

### Using namespaced resolvers

```typescript
import { resolvers, typeDefs } from '@boardroom-sdk/compound'

const apolloClient = new ApolloClient({
  cache: new InMemoryCache(),
  resolvers,
  typeDefs
})

const query = gql`
  query {
    getCompoundProposals @client {
      id
    }
  }
`

const { data: { getCompoundProposals: cProposals } } = await apolloClient.query({ query })
```

### Using non-namespaced resolvers

```typescript
import { unnamespacedResolvers, typeDefs } from '@boardroom-sdk/compound'

const apolloClient = new ApolloClient({
  cache: new InMemoryCache(),
  resolvers: unnamespacedResolvers,
  typeDefs
})

const query = gql`
  query {
    getProposals @client {
      id
    }
  }
`

const { data: { getProposals: cProposals } } = await apolloClient.query({ query })
```

