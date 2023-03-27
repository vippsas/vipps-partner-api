<!-- START_METADATA
---
title: Quick start for the Partner API
sidebar_label: Quick start
sidebar_position: 20
description: Quick start guide for the using the Partner API with Postman.
pagination_next: null
pagination_prev: null
---
END_METADATA -->

# Quick start

Use the Partner API to get details for their own sales units and merchants.
In addition, you can order products on behalf of your merchants.

Be aware that these are running on the production server.

<!-- START_COMMENT -->

ℹ️ Please use the website:
[Vipps MobilePay Technical Documentation](https://developer.vippsmobilepay.com/).

## Table of contents

* [Postman](#postman)
  * [Prerequisites](#prerequisites)
  * [Step 1: Get the Postman collection and environment](#step-1-get-the-postman-collection-and-environment)
  * [Step 2: Import the Postman files](#step-2-import-the-postman-files)
  * [Step 3: Set up Postman environment](#step-3-set-up-postman-environment)
* [Make API calls](#make-api-calls)
  * [Get sales unit by Merchant Serial Number](#get-sales-unit-by-merchant-serial-number)
  * [Get merchant by organization number](#get-merchant-by-organization-number)
  * [Order products on behalf of merchants](#order-products-on-behalf-of-merchants)

<!-- END_COMMENT -->

## Postman

### Prerequisites

Review
[Quick start guides](https://developer.vippsmobilepay.com/docs/vipps-developers/quick-start-guides) for information about getting your test environment set up.

### Step 1: Get the Postman collection and environment

Save the following files to your computer:

* [Partner API Postman collection](tools/vipps-partner-api-postman-collection.json)
* [Global Postman environment](https://raw.githubusercontent.com/vippsas/vipps-developers/master/tools/vipps-api-global-postman-environment.json)

### Step 2: Import the Postman files

1. In Postman, click *Import* in the upper-left corner.
1. In the dialog that opens, with *File* selected, click *Upload Files*.
1. Select the two files you have just downloaded and click *Import*.

### Step 3: Set up Postman environment

**Important:** Partner keys must be kept secret. They can be used to act on behalf
of all the partner's merchants. It is the partner's responsibility to manage
the partner keys in a secure way. See
[Partner keys](https://developer.vippsmobilepay.com/docs/vipps-partner/partner-keys).

1. Click the down arrow, next to the "eye" icon in the top-right corner, and select the environment you have imported.
2. Click the "eye" icon and, in the dropdown window, click `Edit` in the top-right corner.
3. Fill in the `Current Value` for the following fields to get started.
   * `client-id` - Partner key is required for getting the access token.
   * `client-secret` - Partner key is required for getting the access token.
   * `Ocp-Apim-Subscription-Key` - Partner subscription key is required for all requests.
   * `merchantSerialNumber` - Merchant ID is only required for `Get sales unit details based on MSN`, but can be included in all headers.
   * `orgno` -The Organization number for the merchant. It is only used in `Get merchant by organization number`.
   * `base_url_production` - Set to: `https://api.vipps.no`.

  The Partner API only works in the production environment, so `base_url` is set to `api.vipps.no`.

## Make API calls

Be aware that these are running on the production server.

Here is a proposed order of steps, but you can send most of these requests independently of each other.
See the
[API reference](https://developer.vippsmobilepay.com/api/partner)
for details about the calls.

### Get sales unit by Merchant Serial Number

1. Send request `Get Access Token`. This provides you with access to the API.
   Be sure to use the address to the production server and provide keys for a production sales unit.

1. Send request `Get sales unit details based on MSN`. This returns a JSON structure with the details, including the org number. If necessary, update `orgno` in the environment. See [`GET:v0/salesunits/:msn/`](https://developer.vippsmobilepay.com/api/partner#tag/Sales-units/operation/getMSN).

### Get merchant by organization number

1. Send request `Get merchant by organization number` for details about the merchant. See [`GET:v0/merchants/:orgno`](https://developer.vippsmobilepay.com/api/partner#tag/Merchants/operation/getMerchant).

### Order products on behalf of merchants

1. Review the `Order products on behalf of merchants` to see an example of ordering products. Since this is running on the production server, you might not want to run it.  See [`POST:v0/products/orders`](https://developer.vippsmobilepay.com/api/partner#tag/Vipps-Product-Orders/operation/orderProduct).
