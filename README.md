---
description: >-
  This documentation is a place for developers looking to integrate or build on
  top of Boardroom using the Boardroom API and Governance SDK.
---

# Welcome

![](.gitbook/assets/full-logo-dark.png)

Boardroom is a protocol-agnostic governance and management platform built to improve distributed decision-making across crypto networks. The platform is home to hundreds of **DAOs**, helping their members frictionlessly participate in their governance.

Find some options below on how we can work together. If you need some inspiration, check out our [Featured Partners](featured-partners.md) section.

## Integrate Your Protocol with Boardroom

If you are looking to add support for your protocol within Boardroom, you'll need to create an integration in [The Governance SDK](sdk/governance-sdk.md). Integrated protocols within the Governance SDK will be included in the aggregated data served by the [Boardroom API](boardroom-api/boardroom-api.md) and accessible in the Boardroom Portal.

To see if your project is already integrated, check out our [Supported Protocols](protocols.md) page.

{% page-ref page="sdk/integrating-your-protocol.md" %}

## Integrate Governance Data In Your Application

Boardroom provides [The Boardroom API](boardroom-api/boardroom-api.md) as an open, public resource for anybody looking to use our aggregated governance data \(provided by the [Governance SDK](sdk/governance-sdk.md)\) in their client or server applications. Use our HTTP API to fetch governance data for specific protocols or aggregated across multiple protocols that we support.

{% page-ref page="boardroom-api/boardroom-api.md" %}

### Directly Integrate with the Governance SDK

The [Boardroom API](boardroom-api/boardroom-api.md) provides the fastest and simplest way to begin integrating governance data in your applications. However, if you are looking to allow client-side governance interactions such as submitting on-chain proposals or votes or signaling on off-chain platforms like Snapshot, you can directly use the [Governance SDK](sdk/governance-sdk.md) in your browser-based dApp.

{% page-ref page="sdk/quick-start.md" %}

