---
description: >-
  Free and open access to Boardroom's aggregated governance data for your
  applications.
---

# Boardroom API

We believe that free and open access to aggregated governance data is a crucial tool in navigating the rapidly growing ecosystem of stakeholder owned crypto networks. The Boardroom API is a centralized HTTP API that uses the open-source [Governance SDK](../sdk/governance-sdk.md) to continually index and aggregate governance data across all integrated protocols at scale.

{% hint style="success" %}
We are working finalizing our interoperability layer powered by the Governance SDK before making our HTTP API publicly available. If you are looking to integrate governance data into your application, get in touch with us on [Discord](https://discord.gg/UBqtEddhsC), we'd love to hear your ideas and talk about what we have in store 🚀
{% endhint %}

## List All Protocols

{% api-method method="get" host="https://api.boardroom.com/v1" path="/protocols" %}
{% api-method-summary %}
Get a paginated list of all integrated protocols and basic stats
{% endapi-method-summary %}

{% api-method-description %}
Get information about all integrated protocols
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="" type="string" required=false %}

{% endapi-method-parameter %}
{% endapi-method-path-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```
{
  "nextCursor": "ZGVjZW50cmFsZ2FtZXM6ZGVmYXVsdA==",
  "items": [
    {
      "cname": "compound",
      "name": "Compound",
      "totalProposals": 46,
      "totalVotesCast": 2633,
      "tokens": [
        {
          "symbol": "COMP",
          "contractAddress": "0xc00e94Cb662C3520282E6f5717214004A7f26888",
          "marketPrice": [
            { "currency": "usd", "amount": 561.13 }
          ]
        }
      ]
    }
  ]
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

## Get Protocol Details

## List Protocol Proposals

## List Proposal Votes

## Get Voter Profile

## Get Proposal Timeline

