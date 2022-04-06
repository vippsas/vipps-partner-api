# Vipps Partner API

The Vipps Partner API lets partners use their partner keys to retrieve information
about their merchants and their sale units.

API version: 0.0.1.

Document version 0.0.1

## Table of contents
* [Table of contents](#table-of-contents)
* [Information for Vipps partners](#information-for-vipps-partners)
* [Partner keys](#partner-keys)
* [Get information about a merchant based on organization number](#get-information-about-a-merchant-based-on-organization-number)
  * [Future improvements](#future-improvements)
  * [In the meantime](#in-the-meantime)
* [Get information about a sale unit based on MSN](#get-information-about-a-sale-unit-based-on-msn)
  * [Future improvements](#future-improvements)
  * [In the meantime](#in-the-meantime)
* [Questions?](#questions)

## Information for Vipps partners

Please see:
* [Vipps Partners](https://github.com/vippsas/vipps-partner): Technical information for Vipps partners.
* [How to become a Vipps partner](https://vipps.no/developer/bli-partner/) (in Norwegian).

## Partner keys

This API requires
[partner keys](https://github.com/vippsas/vipps-partner#partner-keys).

## Get information about a merchant based on organization number

[`GET:/merchants/{orgno}`](https://vippsas.github.io/vipps-partner-api/#/Merchants/getMerchant)

This endpoint is for retrieving information about the merchant.
In the current version of the Partner API this only returns a list of MSNs
connected to the partner making the API request.

```
{
  "msn": [
    "123456"
  ]
}
```

### Future improvements

Future versions of the API will probably_ return more information, such as:
* Company address
* Contact information for the main person
* Contact information for the technical person
* A list of people with admin rights on portal.vipps.no

Since the response only contains a list of MSNs, an additional API request is
required to get more details about the sale unit.
This is an endpoint for getting information about the _merchant_, not all the
merchant's MSNs.
See:
[Get information about a sale unit based on MSN](#get-information-about-a-sale-unit-based-on-msn).

### In the meantime

All merchants can retrieve their information on
[portal.vipps.no](https://portal.vipps.no).

Merchants can create a user for their parter on
[portal.vipps.no](https://portal.vipps.no),
so the partner can do this directly
as described here:
[Partner keys](https://github.com/vippsas/vipps-partner#partner-keys)
and
[How to add a user on portal.vipps.no](https://github.com/vippsas/vipps-partner/blob/main/add-portal-user.md).

## Get information about a sale unit based on MSN

[`GET:/saleunits/{msn}`](https://vippsas.github.io/vipps-partner-api/#/Salesunits/getMSN)

This endpoint is for retrieving details about one sale unit.

In the current version of the API this only returns basic information:

```
{
  "msn": "123456",
  "name": "Example AS",
  "orgno": "912345678"
}
```

### Future improvements

Future versions of the API will probably_ return more information, such as:
* Vipps products: Which Vipps products are available for this sale unit (eCom, Recurring, Login, etc)
* Capture type: Direct capture or reserve capture. See:
  [eCom FAQ: What is the difference between "Reserve Capture" and "Direct Capture"?](https://github.com/vippsas/vipps-ecom-api/blob/master/vipps-ecom-api-faq.md#what-is-the-difference-between-reserve-capture-and-direct-capture)
* Is `skipLandingPage` available? See:
  [eCom FAQ: Is it possible to skip the landing page?](https://github.com/vippsas/vipps-ecom-api/blob/master/vipps-ecom-api-faq.md#is-it-possible-to-skip-the-landing-page)
* Bank account for settlements
* Settlement frequency
* Settlement type: gross or net
* Transaction cost (price package)
* Status: Active or deactivated

### In the meantime

Until more functionality is available in this API, there are some workarounds:

* Is the MSN set up with "reserve capture" or "direct capture"?  
  See:
  [How can I check if I have "reserve capture" or "direct capture"?](https://github.com/vippsas/vipps-ecom-api/blob/master/vipps-ecom-api-faq.md#how-can-i-check-if-i-have-reserve-capture-or-direct-capture)
* Is the MSN set up with `skipLandingPage`?  
  See:
  [How can I check if I have skipLandingPage activated?](https://github.com/vippsas/vipps-ecom-api/blob/master/vipps-ecom-api-faq.md#how-can-i-check-if-i-have-skiplandingpage-activated)
* Which price is the MSN set up with?
* Which Vipps products does the MSN have access to?  
  See:
  [Getting started: API products](https://github.com/vippsas/vipps-developers/blob/master/vipps-getting-started.md#api-products)

## Questions?

We're always happy to help with code or other questions you might have!
Please create an [issue](https://github.com/vippsas/vipps-api-api/issues),
a [pull request](https://github.com/vippsas/vipps-part-api/pulls),
or [contact us](https://github.com/vippsas/vipps-developers/blob/master/contact.md).

Sign up for our [Technical newsletter for developers](https://github.com/vippsas/vipps-developers/tree/master/newsletters).
