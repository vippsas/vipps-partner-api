# Vipps Merchant Management API

💥 DRAFT! Unfinished work in progress. Useless except for discussions in and with Vipps. 💥

**Background:** There are many things that could and should have been improved in the
[Signup API](https://github.com/vippsas/vipps-signup-api).
Since the API's feature set is rather small, we are planning a new API (this one)
for both partners, banks and large corporations. The current list of priorities are:
1. Functionality to retrieve data about a partner's merchants
   ([`GET:/merchants/{orgno}`](https://vippsas.github.io/vipps-merchant-management-api/#/Merchants/getMerchantDetails))
   and the merchants' sale units
   (([`GET:/merchants/{orgno}/saleunits/{msn}`](https://vippsas.github.io/vipps-merchant-management-api/#/Saleunits/getSaleUnitsByMsn)).
   This will eliminate all the manual emails, Slack message and calls to Partnerbestilling just to ask for info.
2. Functionality to update a sale unit.
   Changes to a merchant requires BankID login to portal.vipps.no, but a partner should be
   able to make changes to the sale units connected to the partner: Name, capture type, etc.
3. Functionality to sign up a new merchant and create a new sale unit.
   This requires BankID login to portal.vipps.no, as there are regulatory requirements that
   comlicate making an API for this. Our opinion is that the current signup functionality on
   portal.vipps.no is simple and "good enough" that this functionality can have a lower priority.


----

This repository contains developer resources for the Vipps Merchant Management API.

* [Vipps Merchant Management API guide](vipps-merchant-management-api.md): Developer guide for Vipps Merchant Management API.

For more information:
* [Vipps Developers](https://github.com/vippsas/vipps-developers): The starting point for Vipps developers.
* [Getting Started](https://github.com/vippsas/vipps-developers/blob/master/vipps-getting-started.md): Information about API keys, product activation.

You can peruse the API reference documentation as:
* [Swagger UI](https://vippsas.github.io/vipps-merchant-management-api/)
* [ReDoc](https://vippsas.github.io/vipps-merchant-management-api/redoc.html)

# Questions?

We're always happy to help with code or other questions you might have!
Please create an [issue](https://github.com/vippsas/vipps-ecom-api/issues),
a [pull request](https://github.com/vippsas/vipps-ecom-api/pulls),
or [contact us](https://github.com/vippsas/vipps-developers/blob/master/contact.md).

Sign up for our [Technical newsletter for developers](https://github.com/vippsas/vipps-developers/tree/master/newsletters).
