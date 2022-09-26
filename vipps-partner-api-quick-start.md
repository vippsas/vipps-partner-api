<!-- START_METADATA
---
title: Quick start
sidebar_position: 20
---
END_METADATA -->

# Quick start

<!-- START_TOC -->

## Table of Contents

* [Postman](#postman)
  * [Prerequisites](#prerequisites)
  * [Step 1: Get the Postman collection](#step-1-get-the-postman-collection)
  * [Step 2: Import the Postman environment](#step-2-import-the-postman-environment)
  * [Step 3: Set up Postman environment](#step-3-set-up-postman-environment)
* [Make API calls](#make-api-calls)
* [Questions?](#questions)

<!-- END_TOC -->

Document version 1.0.2.

## Postman

### Prerequisites

* If you are not familiar with Postman, review
[Getting started with Postman](https://vippsas.github.io/vipps-developer-docs/docs/vipps-developers/vipps-quick-start-guides#getting-started-with-postman).

* You will need a merchant test account.
If you haven't already set this up, see
[Test Merchants](https://vippsas.github.io/vipps-developer-docs/docs/vipps-developers/vipps-test-environment#test-merchants).

### Step 1: Get the Postman collection

Import the collection by following the steps below:

1. Click `Import` in the upper-left corner.
2. Import the [vipps-partner-api-postman-collection.json](tools/vipps-partner-api-postman-collection.json) file.

### Step 2: Import the Postman environment

1. Click `Import` in the upper-left corner.
2. Import the [vipps-partner-api-postman-environment.json](tools/vipps-partner-api-postman-environment.json) file.

### Step 3: Set up Postman environment

1. Click the down arrow, next to the "eye" icon in the top-right corner, and select the environment you have imported.
2. Click the "eye" icon and, in the dropdown window, click `Edit` in the top-right corner.
3. Fill in the `Current Value` for the following fields to get started.
   - `client-id` - Partner key is required for getting the access token.
   - `client-secret` - Partner key is required for getting the access token.
   - `Ocp-Apim-Subscription-Key` - Partner subscription key is required for all requests.
   - `merchantSerialNumber` - Merchant ID is only required for `Get sale unit details based on MSN`, but can be included in all headers.
   - `orgno` -The Organization number for the merchant. It is only used in `Get merchant by organization number`.

  The Partner API only works in the production environment, so `base_url` is set to `api.vipps.no`.

## Make API calls

Be aware that these are running on the production server.
Here is a proposed order of steps, but you can send most of these requests independently of each other.

1. Send request `Get Access Token`. This provides you with access to the API.
2. Send request `Get sale unit details based on MSN`. This returns a JSON structure with the details, including the org number. If necessary, update `orgno` in the environment. See [`GET:v0/salesunits/:msn/`](https://vippsas.github.io/vipps-developer-docs/api/partner#tag/Sales-units/operation/getMSN).
3. Send request `Get merchant by organization number` for details about the transaction. See [`GET:v0/merchants/:orgno`](https://vippsas.github.io/vipps-developer-docs/api/partner#tag/Merchants/operation/getMerchant).
4. Review the `Order products on behalf of merchants` to see an example of ordering products. Since this is running on the production server, you might not want to run it.  See [`POST:v0/products/orders`](https://vippsas.github.io/vipps-developer-docs/api/partner#tag/Vipps-Product-Orders/operation/orderProduct).

See the
[API reference](https://vippsas.github.io/vipps-developer-docs/api/partner)
for details about the calls.

## Questions?

We're always happy to help with code or other questions you might have!
Please create an [issue](https://github.com/vippsas/vipps-partner-api/issues),
a [pull request](https://github.com/vippsas/vipps-partner-api/pulls),
or [contact us](https://github.com/vippsas/vipps-developers/blob/master/contact.md).

Sign up for our [Technical newsletter for developers](https://github.com/vippsas/vipps-developers/tree/master/newsletters).
