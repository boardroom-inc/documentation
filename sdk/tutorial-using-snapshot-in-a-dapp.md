# Tutorial: using Snapshot in a dApp

## Usage

The Snapshot package is protocol agnostic. You can use it with any protocol that has Snapshot support by passing the correct arguments. The list of supported protocols can be found on [https://snapshot.page](https://snapshot.page/#/)

Many of these require passing the name of the protocol to query. The correct name to use is the one corresponding to the name of the Snapshot space. The simplest way to find this is to go to the protocol's page from [https://snapshot.page](https://snapshot.page/#/) and get the name used in the url (i.e. `cream-finance.eth` for Cream protocol). In some cases the SDK can accept multiple names, for instance `yam` or `yam.eth` will both work for Yam protocol.

### Proposals

```typescript
import { Snapshot } from '@boardroom-sdk/sdk';

const snapshot = new Snapshot()

const aaveProposals = await snapshot.getProposals("aave");
const yamProposals = await snapshot.getProposals("yam.eth");
```

### Voters

```typescript
import { Snapshot } from '@boardroom-sdk/sdk';

const snapshot = new Snapshot()

// All Yam voters
const allYamVoters = await snapshot.getSnapshotVoters(
      "yam.eth",
    );
    
// Voters for the specified poll
const yamVotersByPoll = await snapshot.getSnapshotVotersByPoll(
      "yam.eth",
      "QmPsDrBwJYEb6Row6aqruxHZJGqr58HpmqMD7jsGpbUdTu"
    );
```

### Scores

You can query for the total voting power \(score\) for each of a list of addresses. This requires an ethereum provider url to be provided in the class constructor or in the context of the query if querying an apollo client directly.

```typescript
import { Snapshot } from '@boardroom-sdk/sdk';
const snapshot = new Snapshot(ETH_PROVIDER_URL);

const data = await snapshot.getScores(
      "rarible",
      [
        "0x5C2Cb5db7461a4773b3aBACad11ca765196Ac550",
        "0x44aeE4055cb287cCE2050644507105032706b1FA",
        "0x770F83057bd7C39DD598066A0E1235AbCDdf6933"
      ]
    );
/*
returns:
    [
      {
        address: '0x5C2Cb5db7461a4773b3aBACad11ca765196Ac550',
        score: 93.89530922338801,
        __typename: 'SnapshotScore'
      },
      {
        address: '0x44aeE4055cb287cCE2050644507105032706b1FA',
        score: 43.620989315160784,
        __typename: 'SnapshotScore'
      },
      {
        address: '0x770F83057bd7C39DD598066A0E1235AbCDdf6933',
        score: 0,
        __typename: 'SnapshotScore'
      }
    ]
*/
```

You can also get a list of scores for an individual address itemized by strategy name

```typescript
import { Snapshot } from '@boardroom-sdk/sdk';
const snapshot = new Snapshot(ETH_PROVIDER_URL);

const data = await snapshot.getUserScores(
      "rarible",
      "0xBE4475b0e09a017A2ce7f1b62af078CAC7Bb470F"
    );
/*
returns:
    [
      {
        name: 'erc20-balance-of',
        score: 35.612282612175214,
        __typename: 'SnapshotStrategy'
      }
    ]
*/
```

### Governance Stats

Fetch total proposals, total voters, total ballots and a list of scoring strategies for a given protocol.

```typescript
import { Snapshot } from '@boardroom-sdk/sdk';
const snapshot = new Snapshot(ETH_PROVIDER_URL);

const data = await snapshot.getSnapshotGovernance(
      "rarible",
    );
/*
returns:
{
  totalProposals: 34,
  totalVoters: 924,
  totalVotes: 4620,
  snapshotSpace: 'rarible',
  strategies: [ 'erc20-balance-of' ],
  __typename: 'SnapshotGovernance'
}
*/
```

### Posting a Signal

You can post a signal on a poll through the SDK. In the example a signer is obtained from an injected Web3 instance such as Metamask and used to vote choice 2 for proposal `QmY6FRFwnHugEugA3KQqi3xyNCzncTpZPcFJTXkPHeAg4a` on Akropolis.

```typescript
import { Snapshot } from '@boardroom-sdk/sdk';

const postSnapshotSignal = async () => {
  await (window as any).ethereum.enable();
  const signer = new Web3Provider((window as any).ethereum).getSigner();

  const snapshot = new Snapshot(undefined, { signer });
  const address = await signer.getAddress();

  const mutationResult = await snapshot.castVote(
    address,                                          // user address
    "QmY6FRFwnHugEugA3KQqi3xyNCzncTpZPcFJTXkPHeAg4a", // proposal Id
    "akropolis-delphi",                               // protocol name (Snapshot space)
    2                                                 // proposal choice
  );
};
```
