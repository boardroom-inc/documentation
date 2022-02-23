---
description: >-
  This page will guide you through the information that you'll need to submit in
  step 2.
---

# 1. Review Requirements

These docs will walk you through how to add the necessary project information in a few simple steps, to get your project added to the Boardroom Portal frontend.

{% hint style="info" %}
Make sure that the Governance Framework the project is using is supported by Boardroom. You can check the list of supported frameworks [here](../../sdk/governance-frameworks/#all-frameworks).
{% endhint %}

## Your Project

### 1. Project metadata

Project metadata that you'll be asked for in step 2:

| Property                    | Type                          | Description                                                    |
| --------------------------- | ----------------------------- | -------------------------------------------------------------- |
| `cname`                     | `string`                      | A unique identifier for the project.                           |
| `description`               | `string`                      | A short blurb about the protocol.                              |
| `path`                      | `string`                      | The Boardroom portal slug for the protocol.                    |
| `type`                      | `"snapshot" \| "compoundish"` | The governance type of the protocol.                           |
| `discourseForum.url`        | `string`                      | The URL to the protocol Discourse forum.                       |
| `discourseForum.categoryId` | `string`                      | The category ID of the protocol Discourse forum to be sourced. |
| `treasuryAddress`           | `string`                      | The Ethereum address to the project's Treasury address.        |

### 2. Overview File

Upload an `overview.md` file with a high-level description of your project and its governance process (see [Index](https://github.com/boardroom-inc/protocol-Info/blob/main/protocols/indexCoop/overview.md) for an example) in step 2.

**Overview**&#x20;

* How are you working towards your mission?&#x20;
* Ex: Protocol overview, DAO structure overview

**Governance**

* &#x20;How is your governance structured?
* Is it on-chain or off-chain or both?
* A short blurb about your goverance token.
* How are proposals created and reviewed?

**Additional links**

* Links to your social media profiles&#x20;
* Links to your gov-platform&#x20;
* Any relevant links like your website, whitepaper, etc.

### 3. Forum

After you've specified your Discourse Forum URL and the Category that you want to showcase, we will need you to whitelist our URLs on the Discourse Admin interface:

1. Login as an Admin in your Discourse Forum
2. Click on the dropdown menu on the top right
3. Navigate to Admin Settings
4. Search for ‘cors’ in Settings
5. Add the following URLs:
   1. [https://dgov-staging.netlify.app/](https://dgov-staging.netlify.app)
   2. [https://app.boardroom.info/](http://app.boardroom.info)
   3. \*--dgov-staging.netlify.app

## Submit Information

{% content-ref url="2.-submit-your-metadata.md" %}
[2.-submit-your-metadata.md](2.-submit-your-metadata.md)
{% endcontent-ref %}

