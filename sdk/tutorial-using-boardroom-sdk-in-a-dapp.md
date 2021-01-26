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
import { Compound } from '@boardroom-sdk/sdk';

const compound = new Compound()

const proposalWithIdOne = await compound.getProposal("1")
```

## Step 2: Query data from different protocols

```typescript
import { Proposal } from '@boardroom-sdk/sdk';

const getProposals: Promise<Proposal[]> = async () => {
  const protocols = [
    { name: "compound", instance: new Compound()},
    { name: "yearn", instance: new Yearn()},
    { name: "powerpool", instance: new Powerpool()}
  ];
  
  protocols.reduce(async (prev, current) => {
    return {...prev, [current.name]: await current.getProposals() }
  }, {})
  
  // { compound: [...], yearn: [...], powerpool: [...] }

  return proposals
}
```

In this example, we are getting proposals across Compound, Yearn and Powerpool protocols. Since all protocols share the same interface and `getProposals` is one of its methods, it can be invoked like this.

## Step 3: Filtering, sorting and paginating data

```typescript
  // Defaults to page 1, pageSize 2000 and no filter
  const aProposals = await compound.getProposals()

  // Defaults to page 1, pageSize 2000 and filter by Id, so this will only yield 1 proposal
  const bProposals = await compound.getProposals({ where: { id: '1' }}
  )

  // Defaults to page 1, pageSize 50 and no filter  
  const cProposals = await compound.getProposals({ paginate: { pageSize: 50 }})

  // Defaults to page 2, pageSize 2000 and no filter
  const dProposals = await compound.getProposals({ paginate: { page: 2 }})

  // Page 2, pageSize 100 and filter by no votes against
  const eProposals = await compound.getProposals(
    { where: { againstVotes: '0' }, paginate: { pageSize: 100 }}
  )
  
  // Proposals sorted by "isOpen" in ascendent direction
  const fProposals = compound.getProposals(
    { sort: { keys: ['isOpen'], direction: 'asc' }}
  )
  
  // Proposals sorted first by 'isOpen' and then by 'title' in ascendent direction
  const gProposals = compound.getProposals(
    { sort: { keys: ['isOpen', 'title'], direction: 'asc' }}
  )
  
  // Defaults to page 1, pageSize 2000
  // Query for Compound proposals with againstVotes === '0' AND author === null
  const hProposals = await compound.getProposals({ where: {
    againstVotes: '0',
    author: null
  }, conditionType: 'AND' })
  
  // Defaults to page 1, pageSize 2000
  // Query for Compound proposals with againstVotes === '0' OR author === null
  const iProposals = await compound.getProposals({ where: {
    againstVotes: '0',
    author: null
  }, conditionType: 'OR' })
```

Currently, Boardroom SDK supports basic data filtering, sorting and pagination, by passing an options argument.  It contains a `where` object that holds the properties and values the returned entities should match, and a `conditionType` boolean that can be either `'OR'` or `'AND'` \(if undefined, will default to `'AND'`\). It also contains a `paginate` object and a `sort` object as shown above.

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

