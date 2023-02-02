<!-- START_METADATA
---
title: FAQs
sidebar_position: 45
pagination_next: null
---
END_METADATA -->

# FAQs

The Vipps Partner API lets partners use their partner keys to retrieve information
about their merchants and their sale units.

See the
[Vipps Partner API](vipps-partner-api.md)
for all the details.

See also:
[Vipps API FAQ](https://vippsas.github.io/vipps-developer-docs/docs/vipps-developers/faqs).

See also:
[Getting Started](https://vippsas.github.io/vipps-developer-docs/docs/vipps-developers/vipps-getting-started)
guide.

<!-- START_COMMENT -->

ℹ️ Please use the new documentation:
[Vipps Technical Documentation](https://vippsas.github.io/vipps-developer-docs/).

## Table of contents

* [Why do I get `HTTP 404 Not Found`?](#why-do-i-get-http-404-not-found)
* [When will it be possible to change an existing sale unit?](#when-will-it-be-possible-to-change-an-existing-sale-unit)
* [Questions?](#questions)

<!-- END_COMMENT -->

## Why do I get `HTTP 404 Not Found`?

You will get this error for requests to
[`GET:/merchants/{orgno}`](https://vippsas.github.io/vipps-developer-docs/api/partner#tag/Merchants/operation/getMerchant)
if the merchant does not yet have an active sale unit with you as partner.

See:
[How to check if a merchant is signed up with the partner as partner](https://vippsas.github.io/vipps-developer-docs/docs/vipps-partner#how-to-check-if-a-merchant-is-signed-up-with-the-partner-as-partner).

## When will it be possible to change an existing sale unit?

We are working on this now, as fast as we can!
We know this is a very important feature, but can't give you a release date yet.
The documentation will be updated as soon as we have new information.
We recommend subscribing to the
[Technical newsletter for developers](https://vippsas.github.io/vipps-developer-docs/docs/vipps-developers/newsletters).
