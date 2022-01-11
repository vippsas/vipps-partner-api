# Vipps Partner API PoC

💥 DRAFT! Unfinished work in progress. Close to useless except for discussions in and with Vipps. 💥

----------

## Background

Vipps want to provide more self-service for partners.

There are many things that could and should have been improved in the
[Signup API](https://github.com/vippsas/vipps-signup-api).
Since the Signup API's feature set is rather small, we are looking into a new API (this one)
for both partners, banks and large corporations.

See the main page for partners:
[Vipps partner](https://github.com/vippsas/vipps-partner).

The current list of priorities, which may change at any time, is as described below.

## Priorities: Now

1. All partners should use
   [partner keys](https://github.com/vippsas/vipps-partner#partner-keys).
   Partner keys lets a partner make API calls on behalf of a merchant,
   using the same API keys for all the partner's merchants and sale units.

   There is no need to use separate API keys for each merchant or sale unit,
   and this eliminates the main reason for using the Signup API: Key exchange.

2. Functionality to retrieve active MSNs for a partner's merchant
   ([`GET:/merchants/{orgno}`](https://vippsas.github.io/vipps-partner-api/#/Merchants/getMerchantDetails)).

   This will hopefully, with time and extended functionality, eliminate most emails,
   Slack messages and phone calls to Partnerbestilling just to ask for info.

   See:
   [How to sign up new merchants](https://github.com/vippsas/vipps-partner#how-to-sign-up-new-merchants).


## Priorities: Later

3. Functionality to retrieve information for an active MSNs for a partner's
   merchant. This is not as trivial as it sounds, as there are dependencies
   of underlying systems and data that also need work.

   We expect it will be possible to retrieve information like:
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

## Priorities: At some point

4. Functionality to update a sale unit.

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

   This will eliminate more emails, Slack messages and phone calls to
   Partnerbestilling just to aks for a configuration change.

   In the meantime: All merchants can log in on
   [portal.vipps.no](https://portal.vipps.no)
   and create a new user for a person at the partner, so the partner can
   log in and make changes to the relevant sale unit(s).

5. Functionality to sign up a new merchant and create a new sale unit.

   This requires BankID login to
   [portal.vipps.no](https://portal.vipps.no),
   as there are regulatory requirements tha tprevent us from making an API for this.

   Our goal is to let partners "pre-fill" as much as possible for the merchant,
   but the merchant will have to verify the information and sign with BankID on
   [portal.vipps.no](https://portal.vipps.no).

   Our opinion is that the current signup functionality on
   [portal.vipps.no](https://portal.vipps.no)
   is simple and "good enough" that this functionality can have a lower priority.

**Important:** The properties of `Merchant`, `Sale unit`, `Person` _and other data objects_
will change. They depend on the underlying data model in Vipps.
Think of the current ones as a mix between placeholders and examples.

See also:
[Vipps partners](https://github.com/vippsas/vipps-partner)
for more information for partners.

----------

This repository contains developer resources for the Vipps Partner API PoC.

* [Vipps Partner API PoC guide](vipps-partner-api-poc.md): Developer guide for Vipps Partner API PoC.

For more information:
* [Vipps Developers](https://github.com/vippsas/vipps-developers): The starting point for Vipps developers.
* [Getting Started](https://github.com/vippsas/vipps-developers/blob/master/vipps-getting-started.md): Information about API keys, product activation.

You can peruse the API reference documentation as:
* [Swagger UI](https://vippsas.github.io/vipps-partner-api/)
* [ReDoc](https://vippsas.github.io/vipps-partner-api/redoc.html)

# Questions?

We're always happy to help with code or other questions you might have!
Please create an [issue](https://github.com/vippsas/vipps-ecom-api/issues),
a [pull request](https://github.com/vippsas/vipps-ecom-api/pulls),
or [contact us](https://github.com/vippsas/vipps-developers/blob/master/contact.md).

Sign up for our [Technical newsletter for developers](https://github.com/vippsas/vipps-developers/tree/master/newsletters).
