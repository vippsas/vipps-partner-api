# Vipps Partner API

The Vipps Partner API lets partners use their partner keys to retrieve information
about their merchants and their sale units.

API version: 1.0.0.

Document version 1.5.2.

## Table of contents

* [Information for Vipps partners](#information-for-vipps-partners)
  * [Integrating with this API](#integrating-with-this-api)
  * [Partner keys](#partner-keys)
* [Get information about a merchant based on organization number](#get-information-about-a-merchant-based-on-organization-number)
  * [Future improvements](#future-improvements)
  * [In the meantime](#in-the-meantime)
* [Get information about a sale unit based on MSN](#get-information-about-a-sale-unit-based-on-msn)
  * [Future improvements](#future-improvements)
  * [In the meantime](#in-the-meantime)
* [Submit a product order for a merchant](#submit-a-product-order-for-a-merchant)
  * [Future improvements](#future-improvements)
* [Future plans for this API](#future-plans-for-this-api)
* [Questions?](#questions)

## Information for Vipps partners

* [How to become a Vipps partner](https://vipps.no/developer/bli-partner/) (in Norwegian).
* [Vipps Partners](https://github.com/vippsas/vipps-partner): Technical information for Vipps partners.

### Integrating with this API

Integration should be straight-forward.
Use the
[partner keys](https://github.com/vippsas/vipps-partner#partner-keys).
See the Postman collection and environment, and the
[Postman guide](vipps-partner-postman.md).

The Postman collection can also be used to manually make API calls,
even without an integration in place.

**Please note:** Vipps has limited capacity to handle partners' requests to
"just check something", even though it may be trivial. We therefore recommend
the following priority:
1. Integrate with the Partner API, so the functionality is made available
   in the partner's own admin interface.
2. Use the Partner API manually with the Postman collection provided by Vipps.
3. Ask the merchant to create a user for the partner on portal.vipps.no,
   so the partner can check on behalf of the merchant:
   [How to add a user on portal.vipps.no](https://github.com/vippsas/vipps-partner/blob/main/add-portal-user.md).  
4. See the eCom FAQ for how to check if a sale unit
  [has skipLandingPage](https://github.com/vippsas/vipps-ecom-api/blob/master/vipps-ecom-api-faq.md#how-can-i-check-if-i-have-reserve-capture-or-direct-capture)
  or
  [which capture type it has](https://github.com/vippsas/vipps-ecom-api/blob/master/vipps-ecom-api-faq.md#how-do-i-turn-direct-capture-on-or-off).

### Partner keys

All partners can use their
[partner keys](https://github.com/vippsas/vipps-partner#partner-keys).
to use the Partner API. If you have partner keys, you have access to the
Partner API.

**Please note:** Some partners may need an internal Vipps update of their API
product package to get access. Contact your partner manager if you get errors
indicating this. Please double check your partner keys first, though.

## Get information about a merchant based on organization number

[`GET:/merchants/{orgno}`](https://vippsas.github.io/vipps-partner-api/#/Merchants/getMerchant)

This endpoint is for retrieving information about the merchant.

Sequence diagram:

![Get information about a merchant based on organization number](images/sequence-diagram-get-orgno.png)

In the current version of the Partner API only returns a list of MSNs
connected to the partner making the API request, but we _may_ extend this later.

The response (see the Swagger spec for details):

```
{
  "msn": [
    "123456"
  ]
}
```

This is an endpoint for getting information about the _merchant_, not all the
merchant's MSNs.
Since the response only contains a list of MSNs, an additional API request is
required to get more details about the sale unit.
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

Sequence diagram:

![Get information about a sale unit based on MSN](images/sequence-diagram-get-msn.png)

The response (see the Swagger spec for details):

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

The `orgno` is included to make it possible to find out which merchant a MSN
belongs to, which is useful if only the MSN is known.

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

**Important:** This endpoint is available for all partners in the
production environment, but there may be some minor changes. We will do our
utmost to avoid breaking changes, but we can not guarantee it.
As mentioned in the
[README](https://github.com/vippsas/vipps-partner-api/blob/main/README.md):
This is a new API, so feedback is welcome!
Please try to use GitHub's
[issue](https://github.com/vippsas/vipps-partner-api/issues)
functionality, so we can avoid multiple parallel discussions in various channels.

[`POST:/products/orders`](https://vippsas.github.io/vipps-partner-api/#/Vipps%20Product%20Orders/order-product)

This endpoint lets a partner "pre-fill" the product order form on
[portal.vipps.no](https://portal.vipps.no)
on behalf of a merchant, so the merchant can log in, check the data, and submit
the product order.

When the submitted order has been processed, Vipps sends an email to both the
merchant and the partner, as described on
[Vipps Partners](https://github.com/vippsas/vipps-partner).

Sequence diagram:

![Submit a product order for a merchant](images/sequence-diagram-prefill.png)

Here is a sample request, but as this API is new: Always refer to the
API specification for the details.

```
{
  "orgno": "987654321",
  "salesUnitName": "ACME Fantastic Fitness",
  "salesUnitLogo": "VGhlIGltYWdlIGdvZXMgaGVyZQ==",
  "settlementAccountNumber": "86011117947",
  "pricePackageKey": "posstandard",
  "productType": "VIPPS_PA_NETT",
  "mcc": "5200",
  "annualTurnover": "100000",
  "intendedPurpose": "Gym membership",
  "website": {
    "url": "https://example.com",
    "termsUrl": "https://example.com/terms-and-conditions",
    "testWebSiteUrl": "https://test.example.com",
    "testWebsiteUsername": "test-user",
    "testWebsitePassword": "test-password"
  },
}
```

The merchant can not change the information provided by the partner, so if
something needs to be corrected, the merchant must contact the partner to have
the partner submit a new product order with the correct details.

This may be useful:
[Typical reasons for delays](https://github.com/vippsas/vipps-partner/blob/main/README.md#typical-reasons-for-delays).

### Future improvements

We may allow the merchant to change some of the data pre-filled by the
partner, but this is not trivial. If the merchant changes any data, the
partner must be notified and also get the updated data - then merge&sync that
with the "old" data that was sent in the first place.

## Future plans for this API

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

## Questions?

We're always happy to help with code or other questions you might have!
Please create an [issue](https://github.com/vippsas/vipps-api-api/issues),
a [pull request](https://github.com/vippsas/vipps-part-api/pulls),
or [contact us](https://github.com/vippsas/vipps-developers/blob/master/contact.md).

Sign up for our [Technical newsletter for developers](https://github.com/vippsas/vipps-developers/tree/master/newsletters).
