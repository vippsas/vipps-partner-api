# Vipps Partner API

The Vipps Partner API lets partners use their partner keys to retrieve information
about their merchants and their sale units.

API version: 0.0.2.

Document version 1.0.4.

## Table of contents

* [Information for Vipps partners](#information-for-vipps-partners)
* [About this API: Background and priorities](#about-this-api-background-and-priorities)
  * [Background](#background)
  * [Priorities: Now](#priorities-now)
  * [Priorities: Later](#priorities-later)
  * [Priorities: At some point](#priorities-at-some-point)
* [Partner keys](#partner-keys)
* [Get information about a merchant based on organization number](#get-information-about-a-merchant-based-on-organization-number)
  * [Future improvements](#future-improvements)
  * [In the meantime](#in-the-meantime)
* [Get information about a sale unit based on MSN](#get-information-about-a-sale-unit-based-on-msn)
  * [Future improvements](#future-improvements-1)
  * [In the meantime](#in-the-meantime)
* [Submit a product order for a merchant](#submit-a-product-order-for-a-merchant)  
  * [Future improvements](#future-improvements-2)
* [Questions?](#questions)

## Information for Vipps partners

Please see:
* [Vipps Partners](https://github.com/vippsas/vipps-partner): Technical information for Vipps partners.
* [How to become a Vipps partner](https://vipps.no/developer/bli-partner/) (in Norwegian).

## About this API: Background and priorities

### Background

Vipps want to provide more self-service for partners.

### Priorities: Now

1. Functionality to retrieve active MSNs for merchant connected to this partner:
   [`GET:/merchants/{orgno}`](https://vippsas.github.io/vipps-partner-api/#/Merchants/getMerchantDetails)

2. Functionality for retrieving details about one sale unit based on MSN:
   [`GET:/salesunits/{msn}`](https://vippsas.github.io/vipps-partner-api/#/Salesunits/getMSN)

3. Functionality to sign up a new merchant and create a new sale unit.
   Partners can "pre-fill" as much as possible for the merchant
   [`POST:/products/orders`](https://vippsas.github.io/vipps-partner-api/#/Vipps%20Product%20Orders/order-product),
   but the merchant will have to verify the information and sign with BankID on
   [portal.vipps.no](https://portal.vipps.no).
   See:
   [How to sign up new merchants](https://github.com/vippsas/vipps-partner#how-to-sign-up-new-merchants).

### Priorities: At some point

4. Functionality to update an existing sale unit.

   Changes to a sale unit currently requires BankID login to
   [portal.vipps.no](https://portal.vipps.no)
   but a partner should be able to make changes to the sale units connected to
   the partner.

   Some candidates:
   * Status: Deactivate and activate MSNs
   * Name: Update
   * Capture type: Change from "reserve capture" or "direct capture"
   * Skip landing page: Activate or deactivate
   * Price: Update
   * Logo: Update

   In the meantime:
   Merchants can create a user for their parter on
   [portal.vipps.no](https://portal.vipps.no),
   so the partner can do this directly
   as described here:
   [Partner keys](https://github.com/vippsas/vipps-partner#partner-keys)
   and
   [How to add a user on portal.vipps.no](https://github.com/vippsas/vipps-partner/blob/main/add-portal-user.md).

## Partner keys

This API requires
[partner keys](https://github.com/vippsas/vipps-partner#partner-keys).

If you are using partner keys you have access to the Partner API.

**Please note:** Some partners may need an internal update of their API product package
to get acces. Contact your partner manager if you get errors indicating this.

## Get information about a merchant based on organization number

[`GET:/merchants/{orgno}`](https://vippsas.github.io/vipps-partner-api/#/Merchants/getMerchant)

This endpoint is for retrieving information about the merchant.
In the current version of the Partner API only returns a list of MSNs
connected to the partner making the API request, but we _may_ extend this later.

```
{
  "msn": [
    "123456"
  ]
}
```

Since the response only contains a list of MSNs, an additional API request is
required to get more details about the sale unit.
This is an endpoint for getting information about the _merchant_, not all the
merchant's MSNs.
See:
[Get information about a sale unit based on MSN](#get-information-about-a-sale-unit-based-on-msn).

### Future improvements

Future versions of the API will _probably_ return more information,
and we will work with our partners to find out what is useful and possible.
Some candidates:
* Company address
* Contact information for the main person (depends on GDPR, etc)
* Contact information for the technical person (depends on GDPR, etc)
* A list of people with admin rights on portal.vipps.no (depends on GDPR, etc)
* Changelog: What was changed when by who?

### In the meantime

All merchants can see and manage their information on
[portal.vipps.no](https://portal.vipps.no).
Merchants can also see which partner (or PSP) a sale unit is connected to, if any.

Merchants can create a user for their parter on
[portal.vipps.no](https://portal.vipps.no),
so the partner can do this directly as described here:
[Partner keys](https://github.com/vippsas/vipps-partner#partner-keys)
and
[How to add a user on portal.vipps.no](https://github.com/vippsas/vipps-partner/blob/main/add-portal-user.md).

## Get information about a sale unit based on MSN

[`GET:/saleunits/{msn}`](https://vippsas.github.io/vipps-partner-api/#/Salesunits/getMSN)

This endpoint is for retrieving details about one sale unit (MSN).

The current version of the API returns the following information (see the Swagger spec for details):

```
{
  "msn": "123456",
  "name": "ACME Fantastic Fitness",
  "orgno": "987654321",
  "additionalDetails": {
    "skipLandingPage": false,
    "isPureLogin": false,
    "captureType": "ReserveCapture",
    "recurring": false
  }
}
```

The `orgno` is included to make it posible to find out which merchant a MSN belongs to.

### Future improvements

Future versions of the API will _probably_ return more information,
and we will work with our partners to find out what is useful and possible.
Some candidates:

* Vipps products: Which Vipps products and APIs are available for this MSN ("eCom API", "Recurring API", "Login API", etc).
* Transaction cost (price package)
* Status: Active or deactivated

### In the meantime

Until more functionality is available in this API, there are some workarounds:

* [How can I check if I have "reserve capture" or "direct capture"?](https://github.com/vippsas/vipps-ecom-api/blob/master/vipps-ecom-api-faq.md#how-can-i-check-if-i-have-reserve-capture-or-direct-capture)
* [How can I check if I have skipLandingPage activated?](https://github.com/vippsas/vipps-ecom-api/blob/master/vipps-ecom-api-faq.md#how-can-i-check-if-i-have-skiplandingpage-activated)

## Submit a product order for a merchant

[`POST:/products/orders`](https://vippsas.github.io/vipps-partner-api/#/Vipps%20Product%20Orders/order-product)

This endpoint lets a partner "pre-fill" the product order form on
[portal.vipps.no](https://portal.vipps.no)
on behalf of a merchant, so the merchant can log in, check the data, and submit
the product order.

This is some of the information the partner can send (see the API specification
for more):

```
"orgno": "987654321",
"salesUnitName": "My point of sale",
"salesUnitLogo": "VGhlIGltYWdlIGdvZXMgaGVyZQ==",
"settlementAccountNumber": "86011117947",
"pricePackageKey": "posstandard",
"productType": "VIPPS_PA_NETT",
"mcc": "5200",
"annualTurnover": "100000",
"intendedPurpose": "Membership fee for gym",
"website": {
  "url": "https://example.com",
  "termsUrl": "https://example.com/terms-and-conditions",
  "testWebSiteUrl": "https://test.example.com",
  "testWebsiteUsername": "test-user",
  "testWebsitePassword": "test-password"
```

The merchant can not change the information provided by the partner, so if
something needs to be corrected, the merchant must contact the partner to have
the partner submit a new product order with the correct details.

### Future improvements

We may allow the merchant to change some of the data pre-filled by the
partner, but this is not trivial. The updated data must also be made available
for the partner.

## Questions?

We're always happy to help with code or other questions you might have!
Please create an [issue](https://github.com/vippsas/vipps-api-api/issues),
a [pull request](https://github.com/vippsas/vipps-part-api/pulls),
or [contact us](https://github.com/vippsas/vipps-developers/blob/master/contact.md).

Sign up for our [Technical newsletter for developers](https://github.com/vippsas/vipps-developers/tree/master/newsletters).
