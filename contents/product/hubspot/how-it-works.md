---
title: How the Hubspot app works
showTitle: true
---

## What is Hubspot?

Hubspot is a full-featured marketing and CRM platform which includes tools for everything from managing inbound leads to building landing pages. As one of the world’s most popular CRM platforms, Hubspot is an essential PostHog integration for many organizations — and is especially popular with marketing teams.

## How does Hubspot integrate with PostHog?

This PostHog plugin enables you to send user contact data to Hubspot whenever an $identify event occurs. That is, whenever PostHog detects the identity of a user, it can forward that identification information to Hubspot.

Currently, this integration supports sending the following data to Hubspot:

* Email addresses
* First names
* Last names
* Phone numbers
* Company names
* Company website URLs

No other information can currently be sent to PostHog using this plugin. If this plugin exists in a [plugin chain](../../../docs/plugins/build#example-of-a-plugin-chain) where the above information would is filtered out (for example, by using the Property Filter plugin) then filtered information cannot be sent to Hubspot.