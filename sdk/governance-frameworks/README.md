---
description: Details on pre-built governance adapters for common frameworks and services.
---

# Frameworks

Most [protocol integrations](../integrating-your-protocol.md) will not need to implement adapters completely from scratch. For instance, several protocols make use of off-chain signalling for proposals via Snapshot, while others may use a copy of Compound's Governor contracts.

The Governance SDK ships with framework implementations that can be used as adapters by instantiating a framework instance with a minimal set of configuration, keeping protocol integrations very simple.

As the crypto ecosystem evolves and new approaches and frameworks for governance are developed, we can ensure we keep protocol integrations straightforward by staying up to date with our own standardized set of adapters.

{% hint style="info" %}
**Use the pre-built adapters whenever possible in protocol integrations.** This minimizes the chance that you will have to modify your protocol integration in the future, and allows you to leverage the tested and proven existing functionality already in the SDK.
{% endhint %}

## All Frameworks

* [Snapshot](snapshot.md) - Off-chain signaling for proposals
* [Compound Governor Alpha](compound-governor-alpha.md) - Compound on-chain governance
* [Compound Governor Bravo](compound-governor-bravo.md) - Compound on-chain governance
* [Aave Governance V2](aave-governance-v2.md) - Aave on-chain governance
* [Nouns DAO Governor](nouns-dao-governor.md) - Nouns DAO on-chain governance
* [Moloch Governor](moloch-governor.md) - Moloch DAO on-chain governance
* [CoinGecko](coingecko.md) - Token info and market stats
* [Uniswap V2](uniswap-v2.md) - Token market price

{% hint style="info" %}
We're always working to provide pre-built adapters for the most common frameworks, services, and governance contracts in the SDK. Reach out on [Discord](https://discord.gg/UBqtEddhsC) or consider contributing directly to the project if there's a framework you'd like to see supported.
{% endhint %}

