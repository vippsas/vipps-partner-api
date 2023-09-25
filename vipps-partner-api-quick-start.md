<!-- START_METADATA
---
title: Quick start for the Partner API
sidebar_label: Quick start
sidebar_position: 20
description: Quick steps for getting started with the Partner API.
pagination_next: null
pagination_prev: null
---

END_METADATA -->

# Quick start

<!-- START_COMMENT -->
ℹ️ Please use the website:
[Vipps MobilePay Technical Documentation](https://developer.vippsmobilepay.com/docs/APIs/partner-api).
<!-- END_COMMENT -->

## Before you begin

Be aware that these are running on the production server, <https://api.vipps.no>.

🔥 **To reduce risk of exposure, never store production keys in Postman or any similar tools.** 🔥

**Important:** Partner keys must be kept secret. They can be used to act on behalf
of all the partner's merchants. It is the partner's responsibility to manage
the partner keys securely. See
[Partner keys](https://developer.vippsmobilepay.com/docs/partner/partner-keys).

The provided example values in this guide must be changed with the values for your test sales unit and user.
This applies for API keys, HTTP headers, reference, phone number, etc.

## Get information about your merchant sales units

### Step 1 - Setup

You must have already signed up as an organization with Vipps MobilePay and have
your test credentials from the merchant portal.

You will need the following values, as described in the
[Getting started guide](https://developer.vippsmobilepay.com/docs/getting-started):

* `client-id` - Partner key is required for getting the access token.
* `client-secret` - Partner key is required for getting the access token.
* `Ocp-Apim-Subscription-Key` - Partner subscription key is required for all requests.
* `merchantSerialNumber` - The unique ID for a test sales unit. Merchant ID is only required for `Get sales unit details based on MSN`, but can be included in all headers.
* `orgno` -The Organization number for the merchant. It is only used in `Get merchant by organization number`.


### Step 2 - Authentication

For all the following, you will need an `access_token` from the
[Access token API](https://developer.vippsmobilepay.com/docs/APIs/access-token-api):
[`POST:/accesstoken/get`](https://developer.vippsmobilepay.com/api/access-token#tag/Authorization-Service/operation/fetchAuthorizationTokenUsingPost).
This provides you with access to the API.

Note to use the address to the *production* server and provide keys for a *production* sales unit.

```bash
curl https://api.vipps.no/accessToken/get \
-H "client_id: YOUR-CLIENT-ID" \
-H "client_secret: YOUR-CLIENT-SECRET" \
-H "Ocp-Apim-Subscription-Key: YOUR-SUBSCRIPTION-KEY" \
-H "Merchant-Serial-Number: YOUR-MSN" \
-H "Vipps-System-Name: acme" \
-H "Vipps-System-Version: 3.1.2" \
-X POST \
--data ''
```

The property `access_token` should be used for all other API requests in the `Authorization` header as the Bearer token.

### Step 3 - Get merchant by organization number

Send request
[`GET:v0/merchants/{orgno}`](https://developer.vippsmobilepay.com/api/partner#tag/Merchants/operation/getMerchant),
where `orgno` is the organization number of the sales unit.

```bash
curl https://api.vipps.no/partner-api/v0/merchants/{orgno} \
-H "Content-Type: application/json" \
-H "Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1Ni <truncated>" \
-H "Ocp-Apim-Subscription-Key: 0f14ebcab0ec4b29ae0cb90d91b4a84a" \
-H "Vipps-System-Name: acme" \
-H "Vipps-System-Version: 3.1.2" \
-X GET
```

Take note of the merchant serial numbers returned and use one of these in the next step.

### Step 4 - Get sales unit by Merchant Serial Number

Send request
[`GET:v0/salesunits/{msn}/`](https://developer.vippsmobilepay.com/api/partner#tag/Sales-units/operation/getMSN),
where `msn` is the Merchant Serial Number.

This returns a JSON structure with the details, including the org number.

```bash
curl https://api.vipps.no/partner-api/v0/salesunits/{msn} \
-H "Content-Type: application/json" \
-H "Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1Ni <truncated>" \
-H "Ocp-Apim-Subscription-Key: 0f14ebcab0ec4b29ae0cb90d91b4a84a" \
-H "Vipps-System-Name: acme" \
-H "Vipps-System-Version: 3.1.2" \
-X GET
```

### Step 5 - (Example only) Order products on behalf of merchants

See [`POST:v0/products/orders`](https://developer.vippsmobilepay.com/api/partner#tag/Vipps-Product-Orders/operation/orderProduct).

Here is an example using curl. Since this is running on the production server, you might not want to run it.

```bash
curl --location 'https://api.vipps.no/partner-api/v1/products/orders' \
-H "Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1Ni <truncated>" \
--header 'Ocp-Apim-Subscription-Key: 89349472b0e749eabc06ca0255f9f831' \
--header 'Idempotency-Key: 110bc374-976a-4e66-95ed-9a86bda5ab76' \
--header 'Vipps-System-Name: acme' \
--header 'Vipps-System-Version: 2.0' \
--data '{
  "orgno": "123456789",
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
    "testWebSiteUrl": "https://example.com/test ",
    "testWebsiteUsername": "test-user",
    "testWebsitePassword": "test-password"
  },
  "complianceData": {
    "giftCard": {
      "salesPercentage": "TEN_OR_MORE",
      "turnoverShare": "about 25%",
      "validityDuration": "3 years"
    },
    "membership": {
      "turnoverShare": "about 25%",
      "validFor": "YEAR",
      "periodDistribution": "50% yearly 20% monthly"
    },
    "subscription": {
      "turnoverShare": "about 25%",
      "periodDistribution": "50% yearly 20% monthly"
    },
    "course": {
      "turnoverShare": "about 25%",
      "timeBeforeOrder": "10 days",
      "period": "once every 6 week",
      "online": "YES",
      "onlineAccessibleTime": "for 3 months"
    },
    "ticket": {
      "turnoverShare": "about 25%",
      "prepurchaseTime": "10 weeks"
    },
    "rent": {
      "turnoverShare": "about 25%",
      "prepurchaseTime": "15 days",
      "averageRentalDuration": "3 weeks"
    }
  }
}'
```


## Next steps

See the [Partner API guide](vipps-partner-api.md) to read about the concepts and details.
