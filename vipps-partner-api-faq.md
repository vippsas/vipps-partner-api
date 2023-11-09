<!-- START_METADATA
---
title: Partner API Frequently Asked Questions
sidebar_label: FAQ
sidebar_position: 45
description: Frequently asked questions for the Partner API.
pagination_next: null
pagination_prev: null
---
END_METADATA -->

# Frequently asked questions


🔥 The Partner API is deprecated. Please use the [Management API](https://developer.vippsmobilepay.com/docs/APIs/management-api/). 🔥

The Partner API lets partners use their partner keys to retrieve information
about their merchants and their sales units.

See the
[Partner API Guide](vipps-partner-api.md)
for all the technical details.


For general information and questions, please check in the
[Knowledge base](https://developer.vippsmobilepay.com/docs/knowledge-base/).

## Where do I get the pricePackageId?

The `pricePackageId` is a UUID, and you get it when you are activated as partner.
If you have lost it, please search in your email.
If you can not find it, please see
[Questions](https://developer.vippsmobilepay.com/docs/partner#questions)
at the bottom of
[Partners](https://developer.vippsmobilepay.com/docs/partner).

A UUID has a format like this: 81b83246-5c19-7b94-875b-ea6d1114f099.

## Can I use the Partner API in the test environment?

Nope. We do not have all the required backend systems available in the test
environment.

## Why is the URL for a pre-filled product order not working?

If you send an invalid request to
[`POST:/partner-api/v1/products/orders`](https://developer.vippsmobilepay.com/api/partner#tag/Vipps-Product-Orders/operation/orderProduct),
the pre-fill operation will fail, and the URL will lead to the standard, empty
product order form. Although we do *some* input validation, it is not possible
to validate all data.

## Why do I get `HTTP 404 Not Found`?

You will get this error for requests to
[`GET:/partner-api/v0/merchants/{orgno}`](https://developer.vippsmobilepay.com/api/partner#tag/Merchants/operation/getMerchant)
if the merchant does not yet have an active sales unit with you as partner.

See:
[How to check if a merchant is signed up with the partner as partner](https://developer.vippsmobilepay.com/docs/partner#how-to-check-if-a-merchant-is-signed-up-with-the-partner-as-partner).

