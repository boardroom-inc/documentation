# Tutorial: using Snapshot in a dApp

## Usage

The Snapshot package is protocol agnostic. You can use it with any protocol that has Snapshot support by passing the correct arguments. The list of supported protocols can be found on [https://snapshot.page](https://snapshot.page/#/)

### Proposals

```typescript
import { Snapshot } from '@boardroom-sdk/sdk';

const snapshot = new Snapshot()

const aaveProposals = await snapshot.getProposals("aave");
const yamProposals = await snapshot.getProposals("yam");
```

### Voters

```typescript
import { Snapshot } from '@boardroom-sdk/sdk';

const snapshot = new Snapshot()

const yamProposals = await snapshot.getVoters(
      "yam",
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

