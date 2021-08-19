---
description: Documentation for the Boardroom API and Governance SDK.
---

# Introduction

![](.gitbook/assets/full-logo-dark.png)

Boardroom is a protocol-agnostic governance and management platform built to improve distributed decision making across crypto networks. We believe these networks will uproot traditional management and ownership structures. They have already demonstrated a powerful new economic model for building software applications, wherein users build and operate products and services they use every day. In exchange for their contributions, many of these platforms reward users with a direct ownership stake which aligns their success with that of the platform.

With this ownership comes a responsibility to steward governance, communication, and engagement to ensure a powerful alignment between diverse owners.

## Integrate Your Protocol with Boardroom

If you are looking to add support for your protocol within Boardroom, you'll need to create an integration in [The Governance SDK](sdk/governance-sdk.md). Integrated protocols within the Governance SDK will be included in the aggregated data served by the [Boardroom API](boardroom-api/boardroom-api.md) and accessible in the Boardroom Portal.

To see if your project is already integrated, check out our [Supported Protocols](protocols.md) page.

{% page-ref page="sdk/integrating-your-protocol.md" %}

## Integrate Governance Data In Your Application

Boardroom provides [The Boardroom API](boardroom-api/boardroom-api.md) as a open, public resource for anybody looking to use our aggregated governance data \(provided by the [Governance SDK](sdk/governance-sdk.md)\) in their client or server applications. Use our HTTP API to fetch governance data for specific protocols or aggregated across multiple protocols that we support.

### Directly Integrate with the Governance SDK

The [Boardroom API](boardroom-api/boardroom-api.md) provides the fastest and simplest way to begin integrating governance data in your applications. However, if you are looking to allow client-side governance interactions such as submitting on-chain proposals or votes or signaling on off-chain platforms like Snapshot, you can directly use the [Governance SDK](sdk/governance-sdk.md) in your browser-based dApp.

{% page-ref page="sdk/quick-start.md" %}

