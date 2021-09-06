---
description: >-
  The Governance SDK is a protocol and blockchain agnostic governance
  interoperability framework.
---

# Governance SDK

The **Governance SDK** is a portable, protocol-agnostic governance interoperability framework built for NodeJS and the browser. It makes it easier for developers to query and interact with protocol governance in a normalized way by leveraging community-authored protocol integrations.

Both the [Boardroom API](../boardroom-api/boardroom-api.md) and the [Boardroom Portal](../boardroom-portal-1/getting-started.md) use the Governance SDK directly.

{% page-ref page="quick-start.md" %}

{% hint style="info" %}
The Governance SDK is a low-level interop library; it's not well-suited for query data for end-users. 

If you are wanting to build applications or experiences on top of read-only or aggregated governance data, or are not building for a NodeJS or browser environment, **check out the** [**Boardroom API**](../boardroom-api/boardroom-api.md) **for rapidly integrating data sourced by the Governance SDK**.
{% endhint %}

## Integrate Your Protocol

If you are looking to add support for your protocol to the Governance SDK, you'll need to create a new Protocol Integration that implements one or more [Adapters](adapters/).

{% page-ref page="integrating-your-protocol.md" %}

{% hint style="info" %}
We're constantly adding new protocols to our list of [Supported Projects](../protocols.md) -- check this list to see if you're protocol integration has already been implemented by the Boardroom team!
{% endhint %}



