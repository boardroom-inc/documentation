---
description: >-
  Compound is a decentralized money market protocol for borrowing and lending
  assets. It’s an Ethereum protocol that establishes these markets with
  algorithmically set interest rates.
---

# Compound

## The Compound Governance Token <a id="5dd2"></a>

![](../.gitbook/assets/image%20%282%29.png)

Participation starts with the Compound governance token COMP. In addition to being a standard ERC-20 asset, COMP allows the owner to _delegate_ voting rights to the address of their choice; the owner’s wallet, another user, an application, or a DeFi expert. Anybody can participate in Compound governance by receiving delegation, without needing to own COMP. The token also includes code to query an address’ _historical voting weight_, which is useful for building complex voting systems.

## The Governance Framework <a id="5dd2"></a>

![Proposal State Flowchart](../.gitbook/assets/image%20%283%29.png)

Anybody with `1%` of COMP delegated to their address can _`propose`_ a governance action; these are simple or complex sets of actions, such as adding support for a new asset, changing an asset’s collateral factor, changing a market’s interest rate model, or changing any other parameter or variable of the protocol that the [current administrator can modify](https://compound.finance/docs/governance).

Proposals are **executable code**, not suggestions for a team or foundation to implement.

All proposals are subject to a `3 day` voting period, and any address with voting power can vote _for_ or _against_ the proposal. If a majority, and at least 400,000 votes are cast _for_ the proposal, it is queued in the [Timelock](https://app.compound.finance/timelock), and can be implemented after 2 days.

## Resources <a id="5dd2"></a>

* COMP has been deployed to [0xc00e94cb662c3520282e6f5717214004a7f26888](https://etherscan.io/token/0xc00e94cb662c3520282e6f5717214004a7f26888)
* Governance has been deployed to [0xc0dA01a04C3f3E0be433606045bB7017A7323E38](https://etherscan.io/address/0xc0dA01a04C3f3E0be433606045bB7017A7323E38)
* The [COMP and Governance codebase](https://github.com/compound-finance/compound-protocol/releases/tag/v2.5-rc2) is available to review on Github, and has been audited by [OpenZeppelin](https://blog.openzeppelin.com/compound-alpha-governance-system-audit/) and [Trail of Bits](https://github.com/trailofbits/publications/blob/master/reviews/compound-governance.pdf)
* [COMP design assets](https://drive.google.com/drive/u/0/folders/1XiVcOng8v1fbbzrx7N1rqr_o7syDjRST) are available for developers

