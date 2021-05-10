---
description: A high level overview of Boardroom system components and product offerings.
---

# Boardroom Overview

## System Overview

The following diagram illustrates the major components of the Boardroom system and relevant user personas:

![Click to expand](.gitbook/assets/boardroom-systemarch-overview-small.gif)

### Boardroom Portal

Our governance aggregation portal. Powered by the [Boardroom API](boardroom-api/boardroom-api.md) \(for aggregated read-only data\) and the [Governance SDK](sdk/governance-sdk.md) \(for client-side interactions transactions\). Portal Users are protocol stakeholders that want to engage in protocol governance across any of our supported protocols.

{% hint style="info" %}
Checkout the Boardroom Portal [here](https://app.boardroom.info).
{% endhint %}

### Third-party Experience

External applications or experiences built on top of the Boardroom API. These can be apps, platforms, or dApps that want to integrate information or aggregated data about protocol governance for their end users.

Third-party applications can also use the Governance SDK to query data and submit transactions via a normalized programmatic interface that directly access external data sources.

### Boardroom API

A free and publicly accessible HTTP API that surfaces information and aggregated governance data for all protocols integrated with the Governance SDK.

### Governance SDK

An open-source governance interoperability framework. Powers the Boardroom API which uses it to query governance data, and can be used by clients to directly access governance data from downstream data sources.

### Protocol Integrations

Open-source and community-maintained integrations that add support for a protocol to the Governance SDK. Protocol integrations enable querying of governance data and client-side integrations with a protocol's governance framework.

{% page-ref page="sdk/integrating-your-protocol.md" %}

### External Data Sources

Protocol integrations communicate with external data sources such as blockchain networks, traditional web services, TheGraph, IPFS, etc.

### Documentation

You are here! Our documentation is [open-source](https://github.com/boardroom-inc/documentation).

## The Role of The Governance SDK

The Governance SDK is fully open-source and relies on community contributions to support the growing number of protocols in the ecosystem. Its role is to provide abstractions for core governance concepts like proposals, voting, and finance so that client experiences can interact with protocols in a normalized way.

Because of the large volume of data, and some of the challenges involved with directly communicating with the downstream data sources, we built the public and free [Boardroom API](boardroom-api/boardroom-api.md) that aggregates and indexes data in a way that can benefit anybody looking to explore or build experiences on governance data.

{% hint style="info" %}
**Decentralization is important to us at Boardroom,** and we're always looking for ways to make our system more open and resilient as decentralized tech offerings mature in the space.
{% endhint %}

