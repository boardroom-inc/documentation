---
description: >-
  This document is a suggested process for developing and advancing Uniswap
  Governance Proposals. It is a living document intended to be owned, modified
  and enforced by the Uniswap community.
---

# Uniswap

_Note: Autonomous proposals are a recent addition to Governance, not yet considered in this document. A process and policy around this proposal type should be created and implemented by the community._

Process:

Several governance venues available to Uniswap governance are mentioned, each serving its own particular purpose.

1. [gov.uniswap.org](https://gov.uniswap.org/)

[Gov.uniswap.org 17](http://gov.uniswap.org/) is a Discourse forum for governance-related discussion. Community members must register for an account before sharing or liking posts. New members are required to enter 4 topics and read 15 posts over the course of 10 minutes before they are permitted to post themselves.

1. [Snapshot](https://snapshot.page/#/uniswap)

Snapshot is a simple voting interface that allows users to signal sentiment off-chain. Votes on snapshot are weighted by the number of UNI delegated to the address used to vote.

1. Governance Portals

A governance portal can be accessed through the Uniswap [interface 24](https://app.uniswap.org/#/vote). Votes can be delegated and cast through this portal. There are also several other governance interfaces that users can use to cast their votes\*:

* [https://custody.coinbase.com/ ](https://custody.coinbase.com/)
* [http://unigov.eth.link/\#/ap ](http://unigov.eth.link/#/ap)
* [https://app.boardroom.info/](https://app.boardroom.info/)

{% hint style="info" %}
\*Note: this is not a complete list, and should be updated by the community frequently.
{% endhint %}

Below is a preliminary draft for the Uniswap governance process, detailing exactly where these venues fit in. These processes are subject to change according to feedback from the Uniswap community.

**Phase 1: Temperature Check — Discourse/Snapshot**

The purpose of the Temperature Check is to determine if there is sufficient will to make changes to the status quo.

To create a Temperature Check:

1. Ask a general, non-biased question to the community on [gov.uniswap.org 34](http://gov.uniswap.org/) about a potential change \(example: “Should Uniswap governance add liquidity mining for XYZ token?”\). Forum posts should be labeled as follows: “Temperature Check - \[Your Title Here\]”. The forum post should include a link to the associated Snapshot poll.
2. Voters use Snapshot to indicate their interest in bringing it forward to the next stage. Snapshot poll lengths should be set to 3 days.

That’s it! You’ve just started the process of gaining support for a proposal. At the end of the 3 days, a majority vote with a 25k UNI yes-vote threshold wins.

If the Temperature check does not suggest a change from the status quo, the topic will be closed on the governance site. If the Temperature Check does suggest a change, proceed to Stage 2: Consensus Check.

**Phase 2: Consensus Check — Discourse/Snapshot**

The purpose of the Consensus Check is to establish formal discussion around a potential proposal.

To create a Consensus Check:

1. Use feedback from the Temperature Check post and create a new Snapshot poll which covers the options which have gained support. This poll can either be binary or multiple choice but should include the option “Make no change” or its equivalent. Set the poll duration to 5 days.
2. Create a new topic in the Proposal Discussion category on [gov.uniswap.org 34](http://gov.uniswap.org/) titled “Consensus Check — \[Your Title Here\]”. This will alert the community that this topic has already passed Temperature Check. Any topics beginning with Consensus Check that have not passed Temperature Check should be immediately be removed by community moderators. Make sure that the discussion thread links to the new Snapshot poll and the Temperature Check thread.
3. Reach out to your network to build support for the proposal. Discuss the proposal and solicit delegates to vote on it. Be willing to respond to questions on the Consensus Check topic. Share your view point, although try to remain as impartial as possible.

At the end of 5 days, whichever option has the majority of votes wins, and can be included in a governance proposal for Stage 3. A 50k UNI yes-vote quorum is required for the Consensus Check to pass.

If the option “Make no change” wins, the Consensus Check topic should be closed by community moderators.

**Phase 3: Governance Proposal — Governance Portal**

Phase 3 — Governance Proposal — is the final step of the governance process. The proposal should be based on the winning outcome from the Consensus Check and can consist of one or multiple actions, up to a maximum of 10 actions per proposal.

To create a Governance Proposal:

1. Write the code for your proposal, which can be voted on through any Governance Portal. More resources can be found [here 12](https://compound.finance/docs/governance#propose). All proposed code should be audited by a professional auditor. This auditing process could be paid or reimbursed by the community treasury.
2. Ensure at least 10 million UNI is delegated to your address in order to submit a proposal, or find a delegate who has enough delegated UNI to meet the proposal threshold to propose on your behalf.
3. Create a topic in the Proposal Discussion category on [gov.uniswap.org 34](http://gov.uniswap.org/) titled “Governance Proposal \[Proposal Number\] — \[Your Title Here\]” and link to any relevant Snapshot polls/discussion threads as well as the code audit report. Proposal numbers should be in a “UP\#\#\#” format. For example, the first Uniswap Proposal should be titled UP001, the second UP002, and so on. Topics that begin with “Governance Proposal” that have not successfully passed the Temperature Check and Consensus Check stages should be removed by community moderators.
4. Call the propose\(\) function of the Governor Alpha to deploy your proposal.

Once the propose\(\) function has been called, a seven day voting period is started. Ongoing discussion can take place in the [gov.uniswap.org 34](http://gov.uniswap.org/) forum. If the proposal passes successfully, a two day timelock will follow before the proposed code is executed.

**Soft governance:**

The process described above lays out a structure for those wishing to host a formal vote on a particular issue.

However, governance systems also require a degree of “metagovernance” discussions that inform the direction of and the implementation processes behind policy, but which don’t qualify as policy themselves.

The community may discuss new ideas and strategies for governance — including changes to the process outlined above — in the “Governance-Meta” category. On-chain voting is not necessary to make updates to off-chain processes.

**Governance Glossary:**

* UNI: An ERC-20 token that designates the weight of a user’s voting rights. The more UNI a user has in their wallet, the more weight their delegation or vote on a proposal holds.
* Delegation: UNI holders cannot vote or create proposals until they delegate their voting rights to an address. Delegation can be given to one address at a time, including the holder’s own address. Note that delegation does not lock tokens; it simply adds votes to the chosen delegation address.
* Proposal: A proposal is code that is executed by the governance contract through timelock. It can replace the governance contract, transfer tokens from the community treasury, or perform an almost infinite range of other on-chain actions. In order to create a proposal, an address must have at least 1% \(10M UNI\) of all UNI delegated to their address. Proposals are stored in the “proposals” mapping of the Governor smart contract. All proposals are subject to a 7-day voting period. If the proposer does not maintain their vote weight balance throughout the voting period, the proposal may be canceled by anyone.
* Quorum: In order for a vote to pass, at least 4% of all UNI \(40M\) must vote in the affirmative. The purpose of this quorum is to ensure that the only measures that pass have adequate voter participation.
* Voting: Users can vote for or against single proposals once they have voting rights delegated to their address. Votes can be cast while a proposal is in the “Active” state. Votes can be submitted immediately using “castVote” or submitted later with “castVoteBySig” \(For more info on castVoteBySig and offline signatures, see EIP-712\). If the majority of votes \(and a 4% quorum of UNI\) vote for a proposal, the proposal may be queued in the Timelock.
* Voting Period: Once a proposal has been put forward, Uniswap community members will have a seven day period \(the Voting Period\) to cast their votes.
* Timelock: All governance actions are delayed for a minimum of 2 days by the timelock contract before they can be executed.

