---
description: HTTP API request and response reference.
---

# API Reference

{% api-method method="get" host="https://api.boardroom.info" path="/v1/protocols" %}
{% api-method-summary %}
List Protocols
{% endapi-method-summary %}

{% api-method-description %}
Get information about all integrated protocols
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-query-parameters %}
{% api-method-parameter name="pinned" type="string" required=false %}
A CSV list of protocols to include at the top of the results
{% endapi-method-parameter %}

{% api-method-parameter name="cnames" type="string" required=false %}
A CSV list of protocol cnames to include. Other protocols will be filtered out
{% endapi-method-parameter %}

{% api-method-parameter name="limit" type="number" required=false %}
Max number of items to return
{% endapi-method-parameter %}

{% api-method-parameter name="cursor" type="string" required=false %}
Pagination cursor
{% endapi-method-parameter %}
{% endapi-method-query-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
  "data": [
    {
      "cname": "aave",
      "name": "Aave",
      "totalProposals": 17,
      "totalVotes": 900,
      "uniqueVoters": 557,
      "icons": [
        {
          "adapter": "default",
          "size": "thumb",
          "url": "https://assets.coingecko.com/coins/images/12645/thumb/AAVE.png?1601374110"
        },
        {
          "adapter": "default",
          "size": "small",
          "url": "https://assets.coingecko.com/coins/images/12645/small/AAVE.png?1601374110"
        },
        {
          "adapter": "default",
          "size": "large",
          "url": "https://assets.coingecko.com/coins/images/12645/large/AAVE.png?1601374110"
        }
      ],
      "tokens": [
        {
          "adapter": "default",
          "symbol": "aave",
          "network": "ethereum",
          "contractAddress": "0x7fc66500c84a76ad7e9c93437bfc5ac33e2ddae9",
          "marketPrices": [
            {
              "currency": "usd",
              "price": 397.94
            }
          ]
        }
      ]
    },
    {
      "cname": "banklessvault",
      "name": "Bankless DAO",
      "totalProposals": 3,
      "totalVotes": 2538,
      "uniqueVoters": 1598,
      "icons": [
        {
          "adapter": "default",
          "size": "thumb",
          "url": "https://assets.coingecko.com/coins/images/15227/thumb/j4WEJrwU.png?1622615796"
        },
        {
          "adapter": "default",
          "size": "small",
          "url": "https://assets.coingecko.com/coins/images/15227/small/j4WEJrwU.png?1622615796"
        },
        {
          "adapter": "default",
          "size": "large",
          "url": "https://assets.coingecko.com/coins/images/15227/large/j4WEJrwU.png?1622615796"
        }
      ],
      "tokens": [
        {
          "adapter": "default",
          "symbol": "bank",
          "network": "ethereum",
          "contractAddress": "0x2d94aa3e47d9d5024503ca8491fce9a2fb4da198",
          "marketPrices": [
            {
              "currency": "usd",
              "price": 0.02940635
            }
          ]
        }
      ]
    },
    {
      "cname": "compound",
      "name": "Compound",
      "totalProposals": 46,
      "totalVotes": 2633,
      "uniqueVoters": 941,
      "icons": [
        {
          "adapter": "default",
          "size": "thumb",
          "url": "https://assets.coingecko.com/coins/images/10775/thumb/COMP.png?1592625425"
        },
        {
          "adapter": "default",
          "size": "small",
          "url": "https://assets.coingecko.com/coins/images/10775/small/COMP.png?1592625425"
        },
        {
          "adapter": "default",
          "size": "large",
          "url": "https://assets.coingecko.com/coins/images/10775/large/COMP.png?1592625425"
        }
      ],
      "tokens": [
        {
          "adapter": "default",
          "symbol": "comp",
          "network": "ethereum",
          "contractAddress": "0xc00e94cb662c3520282e6f5717214004a7f26888",
          "marketPrices": [
            {
              "currency": "usd",
              "price": 450.38
            }
          ]
        }
      ]
    },
    {
      "cname": "compoundgrants",
      "name": "Compound Grants",
      "totalProposals": 2,
      "totalVotes": 8,
      "uniqueVoters": 7,
      "icons": [
        {
          "adapter": "default",
          "size": "thumb",
          "url": "https://assets.coingecko.com/coins/images/10775/thumb/COMP.png?1592625425"
        },
        {
          "adapter": "default",
          "size": "small",
          "url": "https://assets.coingecko.com/coins/images/10775/small/COMP.png?1592625425"
        },
        {
          "adapter": "default",
          "size": "large",
          "url": "https://assets.coingecko.com/coins/images/10775/large/COMP.png?1592625425"
        }
      ],
      "tokens": [
        {
          "adapter": "default",
          "symbol": "comp",
          "network": "ethereum",
          "contractAddress": "0xc00e94cb662c3520282e6f5717214004a7f26888",
          "marketPrices": [
            {
              "currency": "usd",
              "price": 450.38
            }
          ]
        }
      ]
    },
    {
      "cname": "defidollar",
      "name": "DefiDollar DAO",
      "totalProposals": 5,
      "totalVotes": 10,
      "uniqueVoters": 10,
      "icons": [
        {
          "adapter": "default",
          "size": "thumb",
          "url": "https://assets.coingecko.com/coins/images/12959/thumb/DFD.jpg?1604415975"
        },
        {
          "adapter": "default",
          "size": "small",
          "url": "https://assets.coingecko.com/coins/images/12959/small/DFD.jpg?1604415975"
        },
        {
          "adapter": "default",
          "size": "large",
          "url": "https://assets.coingecko.com/coins/images/12959/large/DFD.jpg?1604415975"
        }
      ],
      "tokens": [
        {
          "adapter": "default",
          "symbol": "dfd",
          "network": "ethereum",
          "contractAddress": "0x20c36f062a31865bed8a5b1e512d9a1a20aa333a",
          "marketPrices": [
            {
              "currency": "usd",
              "price": 0.472084
            }
          ]
        }
      ]
    }
  ],
  "nextCursor": "eyJjbmFtZSI6ImRlZmlkb2xsYXIifQ=="
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="https://api.boardroom.info" path="/v1/protocols/:cname" %}
{% api-method-summary %}
Get Protocol Details
{% endapi-method-summary %}

{% api-method-description %}
Get information about a specific protocol
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="cname" type="string" required=true %}
Protocol cname, e.v. "aave"
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
  "data": {
    "cname": "radicle",
    "name": "Radicle",
    "totalProposals": 4,
    "totalVotes": 64,
    "uniqueVoters": 60,
    "icons": [
      {
        "adapter": "default",
        "size": "thumb",
        "url": "https://assets.coingecko.com/coins/images/14013/thumb/radicle.png?1614402918"
      },
      {
        "adapter": "default",
        "size": "small",
        "url": "https://assets.coingecko.com/coins/images/14013/small/radicle.png?1614402918"
      },
      {
        "adapter": "default",
        "size": "large",
        "url": "https://assets.coingecko.com/coins/images/14013/large/radicle.png?1614402918"
      }
    ],
    "tokens": [
      {
        "adapter": "default",
        "symbol": "rad",
        "network": "ethereum",
        "contractAddress": "0x31c8eacbffdd875c74b94b077895bd78cf1e64a3",
        "marketPrices": [
          {
            "currency": "usd",
            "price": 6.53
          }
        ]
      }
    ]
  }
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="https://api.boardroom.info" path="/v1/proposals" %}
{% api-method-summary %}
List Proposals
{% endapi-method-summary %}

{% api-method-description %}
List proposals across all protocols
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-query-parameters %}
{% api-method-parameter name="cnames" type="string" required=false %}
A CSV list of protocol cnames. Will only include proposals from protocols in this list if provided.
{% endapi-method-parameter %}

{% api-method-parameter name="status" type="string" required=false %}
Filter proposals by their current status. Can be **pending**, **active**, or **closed**
{% endapi-method-parameter %}

{% api-method-parameter name="cursor" type="string" required=false %}
Pagination cursor
{% endapi-method-parameter %}

{% api-method-parameter name="limit" type="number" required=false %}
Max number of items to return
{% endapi-method-parameter %}
{% endapi-method-query-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```

```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="https://api.boardroom.info" path="/v1/protocols/:cname/proposals" %}
{% api-method-summary %}
List Protocol Proposals
{% endapi-method-summary %}

{% api-method-description %}
Get a protocol's proposals
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="cname" type="string" required=true %}
Protocol cname, e.g. "aave"
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}

{% api-method-query-parameters %}
{% api-method-parameter name="status" type="string" required=false %}
Filter proposals by their current status. Can be **pending**, **active**, or **closed**.
{% endapi-method-parameter %}

{% api-method-parameter name="cursor" type="string" required=false %}
Pagination cursor
{% endapi-method-parameter %}

{% api-method-parameter name="limit" type="number" required=false %}
Max number of items to return
{% endapi-method-parameter %}
{% endapi-method-query-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
  "data": [
    {
      "refId": "cHJvcG9zYWw6Y29tcG91bmQ6ZGVmYXVsdDo0Ng==",
      "id": "46",
      "title": "Add LINK Support",
      "content": "LINK is a widely distributed token, with significant liquidity both on and off-chain. As a new market, it will be introduced with the following conservative market parameters: \n - Collateral Factor: 0%\n - Reserve Factor: 25%\n - COMP Speed: 0.0014625 (also set for UNI, BAT, ZRX)\n - Interest Rate Model (JumpRateModelV2)\n - 2% APY borrow base rate\n - 20% APY borrow rate at kink\n - Kink at 80% utilization\n - 100% APY borrow rate at 100% utilization\n\nA 0% collateral factor provides a “no risk” approach to adding the new asset, and allows the protocol to test if the interest rate model and other parameters are a proper fit. Once the market develops there can be an immediate follow-up proposal to increase the collateral factor based on market performance, stress tests etc.\n\nThe Reserve Factor, COMP Speed, and Interest Rate Models were chosen based off the parameters for similar assets (UNI, ZRX, and BAT)\n\n#### Oracle\nThe current oracle and TUSD proposal's new oracle is compatible with LINK there is no change needed.\n\n#### cLINK Contract\nThe cLINK contract is based on the most recently deployed cToken (cWBTC2) implementation, which includes a sweepToken enhancement for governance to collect accidentally sent tokens received by the proxy contract.\n\n#### Special Thanks\n\nSpecial thanks goes out to MasterofNonce for writing the CAP description; Arr00 for helping write simulations; mistertom, jmo, blck, and rleshner for helping decide the parameter proposals; and the community in general for the support and TRiLeZ to organize and deploy the necessery contract and the whole proposal.\n\n#### References\n - [cLINK contract](https://etherscan.io/address/0xface851a4921ce59e912d19329929ce6da6eb0c7#code)\n - [Forums discussion](https://www.comp.xyz/t/add-market-link/1516)\n - [Integration scenario](https://github.com/TRiLeZ/compound-protocol/blob/clink-integration/spec/sim/0010-clink-integration/hypothetical_clink_integration.scen)\n - [Updated mainnet.json](https://github.com/TRiLeZ/compound-protocol/blob/clink-integration/networks/mainnet.json)\n - [Updated token deploy script used](https://github.com/TRiLeZ/compound-protocol/blob/update-deploy-token/script/saddle/deployToken.js)",
      "protocol": "compound",
      "adapter": "default",
      "proposer": "0x54A37d93E57c5DA659F508069Cf65A381b61E189",
      "totalVotes": 36,
      "blockNumber": 12446760,
      "startTime": {
        "blockNumber": 12446760
      },
      "endTime": {
        "blockNumber": 12466470
      },
      "startTimestamp": 1621185107,
      "endTimestamp": 1621449322,
      "choices": [
        "AGAINST",
        "FOR",
        "ABSTAIN"
      ],
      "results": [
        {
          "total": 971696.56,
          "choice": 1
        },
        {
          "total": 18378.75,
          "choice": 2
        }
      ],
      "events": [
        {
          "time": {
            "blockNumber": 12472698
          },
          "event": "queued",
          "timestamp": 1621532858
        },
        {
          "time": {
            "blockNumber": 12485775
          },
          "event": "executed",
          "timestamp": 1621708768
        }
      ]
    },
    {
      "refId": "cHJvcG9zYWw6Y29tcG91bmQ6ZGVmYXVsdDo0NQ==",
      "id": "45",
      "title": "Add TUSD Support",
      "content": "This proposal adds [TrueUSD](https://etherscan.io/token/0x0000000000085d4780B73119b644AE5ecd22b376) as a supported asset.  \n \nTUSD is a 1:1 US dollar backed stablecoin. TUSD is the only stablecoin that has [real-time, 24/7 attestations](https://real-time-attest.trustexplorer.io/trusttoken) from Armanino, a top US accounting firm, providing assurance that the token is fully collateralized by US Dollars. \n \n## Market Parameters \nThis proposal sets TUSD with a collateral factor of 0%, reserve factor of 7.5%, and unlimited borrow cap. These parameters follow the values set by USDT, with 0% collateral factor. The collateral factor can be proposed to be higher with a future proposal. \n \n This proposal updates the Compound price feed to peg TUSD to $1, similarly to USDC. By using a peg, weakness in the underlying asset will not change collateral requirements for users borrowing TUSD.\n \n[The interest rate model](https://etherscan.io/address/0xfb564da37b41b2f6b6edcc3e56fbf523bd9f2012) for TrueUSD relies on the same model as cUSDT and cDAI, JumpRateModelV2. \n \n## Contracts \ncTUSD is an upgradeable cToken contract that has been modified to accommodate potential transfer fees in the underlying token. \n \nThe cToken contract has been reviewed by OpenZeppelin and the Compound team. The cTUSD contract has been reviewed by the TrustToken and Ethworks teams. \n \nThe case for why TUSD benefits compound has been discussed by the [compound community here](https://www.comp.xyz/t/trueusd-listing-proposal-stay-tuned/1490)",
      "protocol": "compound",
      "adapter": "default",
      "proposer": "0x3DdfA8eC3052539b6C9549F12cEA2C295cfF5296",
      "totalVotes": 32,
      "blockNumber": 12444468,
      "startTime": {
        "blockNumber": 12444468
      },
      "endTime": {
        "blockNumber": 12464178
      },
      "startTimestamp": 1621154606,
      "endTimestamp": 1621419034,
      "choices": [
        "AGAINST",
        "FOR",
        "ABSTAIN"
      ],
      "results": [
        {
          "total": 1059354.6,
          "choice": 1
        },
        {
          "total": 22899.395,
          "choice": 2
        }
      ],
      "events": [
        {
          "time": {
            "blockNumber": 12465825
          },
          "event": "queued",
          "timestamp": 1621440489
        },
        {
          "time": {
            "blockNumber": 12479085
          },
          "event": "executed",
          "timestamp": 1621618907
        }
      ]
    },
    {
      "refId": "cHJvcG9zYWw6Y29tcG91bmQ6ZGVmYXVsdDo0NA==",
      "id": "44",
      "title": "Legacy market maintenance: WBTC and REP",
      "content": "In [Proposal 41](https://compound.finance/governance/proposals/41), we began the process to migrate WBTC to a modern upgradable cToken contract.\n\nThe new WBTC cToken has become widely adopted, with $2.2B supplied.\n\nThis proposal continues the deprecation process for the legacy WBTC market, following the process established for SAI and REP.\n\nThe Reserve Factor for the legacy asset will be raised to 100%, which removes the supply interest rate, and supplying and borrowing (new usage) will be disabled. The legacy WBTC cToken will still be effective collateral, and existing users will not be liquidated or materially impacted.\n\nFinally, the proposal completes the deprecation of REP, by lowering its collateral factor to 0%, nine months after [Proposal 17](https://compound.finance/governance/proposals/17) disabled new usage of the asset.\n\n[Discussion](https://www.comp.xyz/t/legacy-market-migration-wbtc/1333)",
      "protocol": "compound",
      "adapter": "default",
      "proposer": "0x54A37d93E57c5DA659F508069Cf65A381b61E189",
      "totalVotes": 54,
      "blockNumber": 12331844,
      "startTime": {
        "blockNumber": 12331844
      },
      "endTime": {
        "blockNumber": 12351554
      },
      "startTimestamp": 1619651997,
      "endTimestamp": 1619915227,
      "choices": [
        "AGAINST",
        "FOR",
        "ABSTAIN"
      ],
      "results": [
        {
          "total": 868928.6,
          "choice": 1
        },
        {
          "total": 5.9100003,
          "choice": 2
        }
      ],
      "events": [
        {
          "time": {
            "blockNumber": 12351969
          },
          "event": "queued",
          "timestamp": 1619920848
        },
        {
          "time": {
            "blockNumber": 12370865
          },
          "event": "executed",
          "timestamp": 1620172850
        }
      ]
    },
    {
      "refId": "cHJvcG9zYWw6Y29tcG91bmQ6ZGVmYXVsdDo0Mw==",
      "id": "43",
      "title": "Governance Analysis Period",
      "content": "Following the upgrade to the [Governor Bravo](https://compound.finance/governance/proposals/42), it's now possible to update the parameters of the Governance system.\n\nOver the past year, a recurring request has been a [formal analysis period](https://www.comp.xyz/t/formal-analysis-period-for-larger-proposals/70) before proposals enter the voting state. This would allow the community and developers additional time to audit new contracts and proposals for errors, and users the opportunity to move COMP or delegations prior to a vote commencing.\n\nThis proposal updates the proposal [voting delay](https://compound.finance/docs/governance#voting-delay) from 1 block to 13140 blocks (2 days), and the voting period from 17280 blocks (2.63 days) to 19710 blocks (3 days). These parameter changes will improve the community’s ability to prepare for votes and increase the security of the protocol.",
      "protocol": "compound",
      "adapter": "default",
      "proposer": "0x8169522c2C57883E8EF80C498aAB7820dA539806",
      "totalVotes": 95,
      "blockNumber": 12235672,
      "startTime": {
        "blockNumber": 12235672
      },
      "endTime": {
        "blockNumber": 12252952
      },
      "startTimestamp": 1618369223,
      "endTimestamp": 1618600389,
      "choices": [
        "AGAINST",
        "FOR",
        "ABSTAIN"
      ],
      "results": [
        {
          "total": 5000,
          "choice": 0
        },
        {
          "total": 1367840.9,
          "choice": 1
        },
        {
          "total": 0,
          "choice": 2
        }
      ],
      "events": [
        {
          "time": {
            "blockNumber": 12253447
          },
          "event": "queued",
          "timestamp": 1618606937
        },
        {
          "time": {
            "blockNumber": 12266840
          },
          "event": "executed",
          "timestamp": 1618785180
        }
      ]
    },
    {
      "refId": "cHJvcG9zYWw6Y29tcG91bmQ6YXJjaGl2ZTo0Mg==",
      "id": "42",
      "title": "Migration to Governor Bravo",
      "content": "### Introduction\nGovernor Bravo has been a community effort for the past few months to bring governance to the next stage. This proposal transfers Compound governance to the new Governor Bravo contract. If this proposal is successful, all future Compound governance calls should be sent to [Governor Bravo](https://etherscan.io/address/0xc0da02939e1441f497fd74f78ce7decb17b66529).\n\n### Proposal Calls\nThe first two calls reimburse Compound Labs $27k that was paid to Open Zeppelin for the audit from the cUSDC reserves. The following two calls award COMP bounties to Arr00 and Blurr for organizing and executing the Governor Bravo project. The following call sets Governor Bravo as the pending admin, and the last call initiates Governor Bravo, accepting the Timelock admin.\n\n### Governor Bravo Details:\nGovernor Bravo has been developed by members of the community in the open for the past few months. The new contracts have been fully audited by Open Zeppelin, are fully covered by extensive test suites, have been simulated by forking simulations, and have been running on the kovan testnet. \n\nThe new features are as follows:\n- Upgradable implementation \n- Settable parameters (proposal threshold, voting period, voting delay)\n- Abstain vote option\n- Optional string voting reason\n- Proposer can always cancel their proposal (until execution)\n- Removal of the guardian\n- Continuous proposal id logic\n\n#### PS:\nTo celebrate the alphas who voted on Governor Alpha, we will be releasing a limited edition Compound NFT claimable by anyone who voted meaningfully on Governor Alpha prior to this proposal once Governor Bravo is initiated.\n\n#### References:\nDevelopment forum [post](https://www.comp.xyz/t/governor-bravo-development/942)\nProposal forum [post](https://www.comp.xyz/t/governor-bravo-proposal/1384)\n[Github PR](https://github.com/compound-finance/compound-protocol/pull/91)\n[Open Zeppelin Audit](https://blog.openzeppelin.com/compound-governor-bravo-audit/)",
      "protocol": "compound",
      "adapter": "archive",
      "proposer": "0xd122638eCa5bB644591fE660FCe0B85E2aB6186a",
      "totalVotes": 59,
      "blockNumber": 12109017,
      "startTime": {
        "blockNumber": 12109017
      },
      "endTime": {
        "blockNumber": 12126297
      },
      "startTimestamp": 1616687925,
      "endTimestamp": 1616917224,
      "choices": [
        "AGAINST",
        "FOR"
      ],
      "results": [
        {
          "total": 1,
          "choice": 0
        },
        {
          "total": 1438679.1,
          "choice": 1
        }
      ],
      "events": [
        {
          "time": {
            "blockNumber": 12127223
          },
          "event": "queued",
          "timestamp": 1616929230
        },
        {
          "time": {
            "blockNumber": 12140390
          },
          "event": "executed",
          "timestamp": 1617104284
        }
      ]
    }
  ],
  "nextCursor": "eyJyZWZJZCI6ImNISnZjRzl6WVd3NlkyOXRjRzkxYm1RNllYSmphR2wyWlRvME1nPT0iLCJzdGFydFRpbWVzdGFtcCI6MTYxNjY4NzkyNX0="
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="https://api.boardroom.info" path="/v1/proposals/:refId" %}
{% api-method-summary %}
Get Proposal Details
{% endapi-method-summary %}

{% api-method-description %}
Get information about a specific proposal
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="refId" type="string" required=true %}
Proposal refId
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
  "data": {
    "refId": "cHJvcG9zYWw6Y29tcG91bmQ6ZGVmYXVsdDo0Ng==",
    "id": "46",
    "title": "Add LINK Support",
    "content": "LINK is a widely distributed token, with significant liquidity both on and off-chain. As a new market, it will be introduced with the following conservative market parameters: \n - Collateral Factor: 0%\n - Reserve Factor: 25%\n - COMP Speed: 0.0014625 (also set for UNI, BAT, ZRX)\n - Interest Rate Model (JumpRateModelV2)\n - 2% APY borrow base rate\n - 20% APY borrow rate at kink\n - Kink at 80% utilization\n - 100% APY borrow rate at 100% utilization\n\nA 0% collateral factor provides a “no risk” approach to adding the new asset, and allows the protocol to test if the interest rate model and other parameters are a proper fit. Once the market develops there can be an immediate follow-up proposal to increase the collateral factor based on market performance, stress tests etc.\n\nThe Reserve Factor, COMP Speed, and Interest Rate Models were chosen based off the parameters for similar assets (UNI, ZRX, and BAT)\n\n#### Oracle\nThe current oracle and TUSD proposal's new oracle is compatible with LINK there is no change needed.\n\n#### cLINK Contract\nThe cLINK contract is based on the most recently deployed cToken (cWBTC2) implementation, which includes a sweepToken enhancement for governance to collect accidentally sent tokens received by the proxy contract.\n\n#### Special Thanks\n\nSpecial thanks goes out to MasterofNonce for writing the CAP description; Arr00 for helping write simulations; mistertom, jmo, blck, and rleshner for helping decide the parameter proposals; and the community in general for the support and TRiLeZ to organize and deploy the necessery contract and the whole proposal.\n\n#### References\n - [cLINK contract](https://etherscan.io/address/0xface851a4921ce59e912d19329929ce6da6eb0c7#code)\n - [Forums discussion](https://www.comp.xyz/t/add-market-link/1516)\n - [Integration scenario](https://github.com/TRiLeZ/compound-protocol/blob/clink-integration/spec/sim/0010-clink-integration/hypothetical_clink_integration.scen)\n - [Updated mainnet.json](https://github.com/TRiLeZ/compound-protocol/blob/clink-integration/networks/mainnet.json)\n - [Updated token deploy script used](https://github.com/TRiLeZ/compound-protocol/blob/update-deploy-token/script/saddle/deployToken.js)",
    "protocol": "compound",
    "adapter": "default",
    "proposer": "0x54A37d93E57c5DA659F508069Cf65A381b61E189",
    "totalVotes": 36,
    "blockNumber": 12446760,
    "startTime": {
      "blockNumber": 12446760
    },
    "endTime": {
      "blockNumber": 12466470
    },
    "startTimestamp": 1621185107,
    "endTimestamp": 1621449322,
    "choices": [
      "AGAINST",
      "FOR",
      "ABSTAIN"
    ],
    "results": [
      {
        "total": 971696.56,
        "choice": 1
      },
      {
        "total": 18378.75,
        "choice": 2
      }
    ],
    "events": [
      {
        "time": {
          "blockNumber": 12472698
        },
        "event": "queued",
        "timestamp": 1621532858
      },
      {
        "time": {
          "blockNumber": 12485775
        },
        "event": "executed",
        "timestamp": 1621708768
      }
    ]
  }
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="https://api.boardroom.com" path="/v1/proposals/:refId/votes" %}
{% api-method-summary %}
List Proposal Votes
{% endapi-method-summary %}

{% api-method-description %}
Get all votes cast for a specific proposal
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="refId" type="string" required=true %}
Proposal refId
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}

{% api-method-query-parameters %}
{% api-method-parameter name="pinned" type="string" required=false %}
A CSV list of addresses that should be included at the top of the results
{% endapi-method-parameter %}

{% api-method-parameter name="limit" type="number" required=false %}
Max number of items to return
{% endapi-method-parameter %}

{% api-method-parameter name="cursor" type="string" required=false %}
Pagination cursor
{% endapi-method-parameter %}
{% endapi-method-query-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
  "data": [
    {
      "refId": "dm90ZTpjb21wb3VuZDpkZWZhdWx0OjQ2OjB4ZWQ0MDljOWZmNjBmMzAyMGFiZjkwMTJiY2Q0NWZjMjk0ZjU2MDhmZg==",
      "proposalRefId": "cHJvcG9zYWw6Y29tcG91bmQ6ZGVmYXVsdDo0Ng==",
      "protocol": "compound",
      "adapter": "default",
      "proposalId": "46",
      "address": "0xeD409c9fF60f3020abF9012bcd45Fc294f5608fF",
      "power": 325761.12,
      "reason": "",
      "choice": 1,
      "time": {
        "blockNumber": 12455528
      },
      "timestamp": 1621302816
    },
    {
      "refId": "dm90ZTpjb21wb3VuZDpkZWZhdWx0OjQ2OjB4NjYyNjU5M2MyMzdmNTMwZDE1YWU5OTgwYTk1ZWY5MzhhYzE1YzM1Yw==",
      "proposalRefId": "cHJvcG9zYWw6Y29tcG91bmQ6ZGVmYXVsdDo0Ng==",
      "protocol": "compound",
      "adapter": "default",
      "proposalId": "46",
      "address": "0x6626593C237f530D15aE9980A95ef938Ac15c35c",
      "power": 126146.29,
      "reason": "",
      "choice": 1,
      "time": {
        "blockNumber": 12459521
      },
      "timestamp": 1621355919
    },
    {
      "refId": "dm90ZTpjb21wb3VuZDpkZWZhdWx0OjQ2OjB4YWM1NzIwZDZlZTJkNzg3MmI4ODkxNGM5YzVmYTliZjM4ZTcyZmFmNg==",
      "proposalRefId": "cHJvcG9zYWw6Y29tcG91bmQ6ZGVmYXVsdDo0Ng==",
      "protocol": "compound",
      "adapter": "default",
      "proposalId": "46",
      "address": "0xAC5720d6EE2d7872b88914C9c5Fa9BF38e72FaF6",
      "power": 105138.67,
      "reason": "",
      "choice": 1,
      "time": {
        "blockNumber": 12453734
      },
      "timestamp": 1621278331
    },
    {
      "refId": "dm90ZTpjb21wb3VuZDpkZWZhdWx0OjQ2OjB4ODE2OTUyMmMyYzU3ODgzZThlZjgwYzQ5OGFhYjc4MjBkYTUzOTgwNg==",
      "proposalRefId": "cHJvcG9zYWw6Y29tcG91bmQ6ZGVmYXVsdDo0Ng==",
      "protocol": "compound",
      "adapter": "default",
      "proposalId": "46",
      "address": "0x8169522c2C57883E8EF80C498aAB7820dA539806",
      "power": 101000.02,
      "reason": "",
      "choice": 1,
      "time": {
        "blockNumber": 12461712
      },
      "timestamp": 1621385394
    },
    {
      "refId": "dm90ZTpjb21wb3VuZDpkZWZhdWx0OjQ2OjB4NTRhMzdkOTNlNTdjNWRhNjU5ZjUwODA2OWNmNjVhMzgxYjYxZTE4OQ==",
      "proposalRefId": "cHJvcG9zYWw6Y29tcG91bmQ6ZGVmYXVsdDo0Ng==",
      "protocol": "compound",
      "adapter": "default",
      "proposalId": "46",
      "address": "0x54A37d93E57c5DA659F508069Cf65A381b61E189",
      "power": 100075.9,
      "reason": "",
      "choice": 1,
      "time": {
        "blockNumber": 12461914
      },
      "timestamp": 1621387993
    }
  ],
  "nextCursor": "eyJyZWZJZCI6ImRtOTBaVHBqYjIxd2IzVnVaRHBrWldaaGRXeDBPalEyT2pCNE5UUmhNemRrT1RObE5UZGpOV1JoTmpVNVpqVXdPREEyT1dObU5qVmhNemd4WWpZeFpURTRPUT09IiwidGltZXN0YW1wIjoxNjIxMzg3OTkzfQ=="
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="https://api.boardroom.com" path="/v1/voters/:address/votes" %}
{% api-method-summary %}
List Voter Votes
{% endapi-method-summary %}

{% api-method-description %}
List all votes cast by a specific voter
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="address" type="string" required=true %}
The wallet address of the voter
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}

{% api-method-query-parameters %}
{% api-method-parameter name="cname" type="string" required=false %}
Only return votes from a specific protocol
{% endapi-method-parameter %}

{% api-method-parameter name="cursor" type="string" required=false %}
Pagination cursor
{% endapi-method-parameter %}

{% api-method-parameter name="limit" type="number" required=false %}
Max number of items to return
{% endapi-method-parameter %}
{% endapi-method-query-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```
{
  "data": [
    {
      "refId": "dm90ZTpjb21wb3VuZDpkZWZhdWx0OjQ2OjB4YWM1NzIwZDZlZTJkNzg3MmI4ODkxNGM5YzVmYTliZjM4ZTcyZmFmNg==",
      "proposalRefId": "cHJvcG9zYWw6Y29tcG91bmQ6ZGVmYXVsdDo0Ng==",
      "protocol": "compound",
      "adapter": "default",
      "proposalId": "46",
      "address": "0xAC5720d6EE2d7872b88914C9c5Fa9BF38e72FaF6",
      "power": 105138.67,
      "reason": "",
      "choice": 1,
      "time": {
        "blockNumber": 12453734
      },
      "timestamp": 1621278331,
      "proposalInfo": {
        "title": "Add LINK Support",
        "startTime": {
          "blockNumber": 12446760
        },
        "endTime": {
          "blockNumber": 12466470
        },
        "startTimestamp": 1621185107,
        "endTimestamp": 1621449322,
        "choices": [
          "AGAINST",
          "FOR",
          "ABSTAIN"
        ],
        "events": [
          {
            "time": {
              "blockNumber": 12472698
            },
            "event": "queued",
            "timestamp": 1621532858
          },
          {
            "time": {
              "blockNumber": 12485775
            },
            "event": "executed",
            "timestamp": 1621708768
          }
        ]
      }
    },
    {
      "refId": "dm90ZTpjb21wb3VuZDpkZWZhdWx0OjQ1OjB4YWM1NzIwZDZlZTJkNzg3MmI4ODkxNGM5YzVmYTliZjM4ZTcyZmFmNg==",
      "proposalRefId": "cHJvcG9zYWw6Y29tcG91bmQ6ZGVmYXVsdDo0NQ==",
      "protocol": "compound",
      "adapter": "default",
      "proposalId": "45",
      "address": "0xAC5720d6EE2d7872b88914C9c5Fa9BF38e72FaF6",
      "power": 105138.67,
      "reason": "",
      "choice": 1,
      "time": {
        "blockNumber": 12453734
      },
      "timestamp": 1621278331,
      "proposalInfo": {
        "title": "Add TUSD Support",
        "startTime": {
          "blockNumber": 12444468
        },
        "endTime": {
          "blockNumber": 12464178
        },
        "startTimestamp": 1621154606,
        "endTimestamp": 1621419034,
        "choices": [
          "AGAINST",
          "FOR",
          "ABSTAIN"
        ],
        "events": [
          {
            "time": {
              "blockNumber": 12465825
            },
            "event": "queued",
            "timestamp": 1621440489
          },
          {
            "time": {
              "blockNumber": 12479085
            },
            "event": "executed",
            "timestamp": 1621618907
          }
        ]
      }
    },
    {
      "refId": "dm90ZTpjb21wb3VuZDpkZWZhdWx0OjQ0OjB4YWM1NzIwZDZlZTJkNzg3MmI4ODkxNGM5YzVmYTliZjM4ZTcyZmFmNg==",
      "proposalRefId": "cHJvcG9zYWw6Y29tcG91bmQ6ZGVmYXVsdDo0NA==",
      "protocol": "compound",
      "adapter": "default",
      "proposalId": "44",
      "address": "0xAC5720d6EE2d7872b88914C9c5Fa9BF38e72FaF6",
      "power": 105137.89,
      "reason": "",
      "choice": 1,
      "time": {
        "blockNumber": 12332418
      },
      "timestamp": 1619659670,
      "proposalInfo": {
        "title": "Legacy market maintenance: WBTC and REP",
        "startTime": {
          "blockNumber": 12331844
        },
        "endTime": {
          "blockNumber": 12351554
        },
        "startTimestamp": 1619651997,
        "endTimestamp": 1619915227,
        "choices": [
          "AGAINST",
          "FOR",
          "ABSTAIN"
        ],
        "events": [
          {
            "time": {
              "blockNumber": 12351969
            },
            "event": "queued",
            "timestamp": 1619920848
          },
          {
            "time": {
              "blockNumber": 12370865
            },
            "event": "executed",
            "timestamp": 1620172850
          }
        ]
      }
    },
    {
      "refId": "dm90ZTpjb21wb3VuZDpkZWZhdWx0OjQzOjB4YWM1NzIwZDZlZTJkNzg3MmI4ODkxNGM5YzVmYTliZjM4ZTcyZmFmNg==",
      "proposalRefId": "cHJvcG9zYWw6Y29tcG91bmQ6ZGVmYXVsdDo0Mw==",
      "protocol": "compound",
      "adapter": "default",
      "proposalId": "43",
      "address": "0xAC5720d6EE2d7872b88914C9c5Fa9BF38e72FaF6",
      "power": 105129.9,
      "reason": "",
      "choice": 1,
      "time": {
        "blockNumber": 12239631
      },
      "timestamp": 1618422394,
      "proposalInfo": {
        "title": "Governance Analysis Period",
        "startTime": {
          "blockNumber": 12235672
        },
        "endTime": {
          "blockNumber": 12252952
        },
        "startTimestamp": 1618369223,
        "endTimestamp": 1618600389,
        "choices": [
          "AGAINST",
          "FOR",
          "ABSTAIN"
        ],
        "events": [
          {
            "time": {
              "blockNumber": 12253447
            },
            "event": "queued",
            "timestamp": 1618606937
          },
          {
            "time": {
              "blockNumber": 12266840
            },
            "event": "executed",
            "timestamp": 1618785180
          }
        ]
      }
    },
    {
      "refId": "dm90ZTpjb21wb3VuZDphcmNoaXZlOjQyOjB4YWM1NzIwZDZlZTJkNzg3MmI4ODkxNGM5YzVmYTliZjM4ZTcyZmFmNg==",
      "proposalRefId": "cHJvcG9zYWw6Y29tcG91bmQ6YXJjaGl2ZTo0Mg==",
      "protocol": "compound",
      "adapter": "archive",
      "proposalId": "42",
      "address": "0xAC5720d6EE2d7872b88914C9c5Fa9BF38e72FaF6",
      "power": 105130.22,
      "choice": 1,
      "time": {
        "blockNumber": 12109242
      },
      "timestamp": 1616690802,
      "proposalInfo": {
        "title": "Migration to Governor Bravo",
        "startTime": {
          "blockNumber": 12109017
        },
        "endTime": {
          "blockNumber": 12126297
        },
        "startTimestamp": 1616687925,
        "endTimestamp": 1616917224,
        "choices": [
          "AGAINST",
          "FOR"
        ],
        "events": [
          {
            "time": {
              "blockNumber": 12127223
            },
            "event": "queued",
            "timestamp": 1616929230
          },
          {
            "time": {
              "blockNumber": 12140390
            },
            "event": "executed",
            "timestamp": 1617104284
          }
        ]
      }
    }
  ],
  "nextCursor": "eyJyZWZJZCI6ImRtOTBaVHBqYjIxd2IzVnVaRHBoY21Ob2FYWmxPalF5T2pCNFlXTTFOekl3WkRabFpUSmtOemczTW1JNE9Ea3hOR001WXpWbVlUbGlaak00WlRjeVptRm1OZz09IiwidGltZXN0YW1wIjoxNjE2NjkwODAyfQ=="
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="https://api.boardroom.info" path="/v1/protocols/:cname/voters" %}
{% api-method-summary %}
List Protocol Voters
{% endapi-method-summary %}

{% api-method-description %}
List voters who have voted at least once for a specific protocol
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="cname" type="string" required=false %}
Protocol cname, eg "compound"
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}

{% api-method-query-parameters %}
{% api-method-parameter name="cursor" type="string" required=false %}
Pagination cursor
{% endapi-method-parameter %}

{% api-method-parameter name="limit" type="number" required=false %}
Max number of items to return
{% endapi-method-parameter %}
{% endapi-method-query-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```
{
  "data": [
    {
      "address": "0xeD409c9fF60f3020abF9012bcd45Fc294f5608fF",
      "firstVoteCast": 1588127130,
      "lastVoteCast": 1621302816,
      "totalVotesCast": 20,
      "protocols": [
        {
          "protocol": "compound",
          "totalVotesCast": 20,
          "lastVoteCast": 1621302816,
          "firstVoteCast": 1588127130,
          "totalPowerCast": 6515510
        }
      ]
    },
    {
      "address": "0x54A37d93E57c5DA659F508069Cf65A381b61E189",
      "firstVoteCast": 1587974682,
      "lastVoteCast": 1621387993,
      "totalVotesCast": 43,
      "protocols": [
        {
          "protocol": "compound",
          "totalVotesCast": 43,
          "lastVoteCast": 1621387993,
          "firstVoteCast": 1587974682,
          "totalPowerCast": 4146452
        }
      ]
    },
    {
      "address": "0x6626593C237f530D15aE9980A95ef938Ac15c35c",
      "firstVoteCast": 1588013872,
      "lastVoteCast": 1621355919,
      "totalVotesCast": 32,
      "protocols": [
        {
          "protocol": "compound",
          "totalVotesCast": 32,
          "lastVoteCast": 1621355919,
          "firstVoteCast": 1588013872,
          "totalPowerCast": 3287531.8
        },
        {
          "protocol": "uniswap",
          "totalVotesCast": 1,
          "lastVoteCast": 1602553638,
          "firstVoteCast": 1602553638,
          "totalPowerCast": 14570243
        }
      ]
    },
    {
      "address": "0xAC5720d6EE2d7872b88914C9c5Fa9BF38e72FaF6",
      "firstVoteCast": 1592519749,
      "lastVoteCast": 1621278331,
      "totalVotesCast": 27,
      "protocols": [
        {
          "protocol": "compound",
          "totalVotesCast": 27,
          "lastVoteCast": 1621278331,
          "firstVoteCast": 1592519749,
          "totalPowerCast": 2840942.5
        }
      ]
    },
    {
      "address": "0x7e4A8391C728fEd9069B2962699AB416628B19Fa",
      "firstVoteCast": 1588018398,
      "lastVoteCast": 1618453041,
      "totalVotesCast": 27,
      "protocols": [
        {
          "protocol": "compound",
          "totalVotesCast": 27,
          "lastVoteCast": 1618453041,
          "firstVoteCast": 1588018398,
          "totalPowerCast": 2601041.8
        },
        {
          "protocol": "uniswap",
          "totalVotesCast": 4,
          "lastVoteCast": 1622833304,
          "firstVoteCast": 1602526282,
          "totalPowerCast": 54288720
        }
      ]
    }
  ],
  "nextCursor": "eyJhZGRyZXNzIjoiMHg3ZTRBODM5MUM3MjhmRWQ5MDY5QjI5NjI2OTlBQjQxNjYyOEIxOUZhIiwicG93ZXIiOjI2MDEwNDEuOH0="
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="https://api.boardroom.info" path="/v1/voters" %}
{% api-method-summary %}
List Voters
{% endapi-method-summary %}

{% api-method-description %}
List all voters across all protocols
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-query-parameters %}
{% api-method-parameter name="cursor" type="string" required=false %}
Pagination cursor
{% endapi-method-parameter %}

{% api-method-parameter name="limit" type="number" required=false %}
Max number of items to return
{% endapi-method-parameter %}
{% endapi-method-query-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```
{
  "data": [
    {
      "address": "0x303EeFeDeE1bA8e5d507a55465d946B2fea18583",
      "firstVoteCast": 1617821053,
      "lastVoteCast": 1623266018,
      "totalVotesCast": 11,
      "protocols": [
        {
          "protocol": "banklessvault",
          "totalVotesCast": 2,
          "lastVoteCast": 1620927129,
          "firstVoteCast": 1620171403,
          "totalPowerCast": 10000
        },
        {
          "protocol": "indexCoop",
          "totalVotesCast": 9,
          "lastVoteCast": 1623266018,
          "firstVoteCast": 1617821053,
          "totalPowerCast": 28.71445
        }
      ]
    },
    {
      "address": "0x8330cC3A4dac3187f76ea4615C13A119a2243521",
      "firstVoteCast": 1621365327,
      "lastVoteCast": 1623265924,
      "totalVotesCast": 10,
      "protocols": [
        {
          "protocol": "indexCoop",
          "totalVotesCast": 10,
          "lastVoteCast": 1623265924,
          "firstVoteCast": 1621365327,
          "totalPowerCast": 702.1724
        }
      ]
    },
    {
      "address": "0xA32E9A93407C629D1a952bdAdc0D2f72887d0326",
      "firstVoteCast": 1607889944,
      "lastVoteCast": 1623265720,
      "totalVotesCast": 57,
      "protocols": [
        {
          "protocol": "indexCoop",
          "totalVotesCast": 55,
          "lastVoteCast": 1623265720,
          "firstVoteCast": 1607889944,
          "totalPowerCast": 19667.178
        },
        {
          "protocol": "uniswap",
          "totalVotesCast": 2,
          "lastVoteCast": 1622790050,
          "firstVoteCast": 1608632887,
          "totalPowerCast": 2438.6416
        }
      ]
    },
    {
      "address": "0x80bF87E5Ef44D943380279142B2B288EAf73a571",
      "firstVoteCast": 1618477655,
      "lastVoteCast": 1623265650,
      "totalVotesCast": 26,
      "protocols": [
        {
          "protocol": "indexCoop",
          "totalVotesCast": 26,
          "lastVoteCast": 1623265650,
          "firstVoteCast": 1618477655,
          "totalPowerCast": 535.33997
        }
      ]
    },
    {
      "address": "0x06Dc0CBF44EED256C5975210095be703504a4541",
      "firstVoteCast": 1620164674,
      "lastVoteCast": 1623265623,
      "totalVotesCast": 4,
      "protocols": [
        {
          "protocol": "banklessvault",
          "totalVotesCast": 4,
          "lastVoteCast": 1623265623,
          "firstVoteCast": 1620164674,
          "totalPowerCast": 209104.66
        }
      ]
    }
  ],
  "nextCursor": "eyJhZGRyZXNzIjoiMHgwNkRjMENCRjQ0RUVEMjU2QzU5NzUyMTAwOTViZTcwMzUwNGE0NTQxIiwidGltZXN0YW1wIjoxNjIzMjY1NjIzfQ=="
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

