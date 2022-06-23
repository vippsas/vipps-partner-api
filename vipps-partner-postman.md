# Postman

[Postman](https://www.getpostman.com/) is a common tool for working with REST APIs.
We offer a [Postman Collection](https://www.getpostman.com/collection) to make development easier.
See the [Postman documentation](https://www.getpostman.com/docs/) for more information about using Postman.

By following the steps below, you can make calls to all the
endpoints, and see the full `request` and `response` for each call.

We also have a short [getting started guide to Postman](https://github.com/vippsas/vipps-developers/blob/master/postman-guide.md).

## Setting up Postman

### Step 1: Get the Postman Collection

Import the collection by following the steps below:

1. Click `Import` in the upper-left corner.
2. Import the [vipps-partner-api-postman-collection.json](https://raw.githubusercontent.com/vippsas/vipps-partner-api/master/tools/vipps-partner-api-postman-collection.json) file.

### Step 2: Import the Postman Environment

1. Click `Import` in the upper-left corner.
2. Import the [vipps-partner-api-postman-environment.json](https://raw.githubusercontent.com/vippsas/vipps-partner-api/master/tools/vipps-partner-api-postman-environment.json) file.

### Step 3: Setup Postman Environment

1. Click the down arrow, next to the "eye" icon in the top-right corner, and select the environment you have imported.
2. Click the "eye" icon and, in the dropdown window, click `Edit` in the top-right corner.
3. Fill in the `Current Value` for the following fields to get started.
   - `client-id`
   - `client-secret`
   - `Ocp-Apim-Subscription-Key`
   - `merchantSerialNumber` - only needed for `Get sale unit details based on MSN`
   - `orgno` - only needed for `Get merchant by organization number`

  The Partner API only works in the production environment, so `base_url` is set to `api.vipps.no`.

### Step 4: Run Tests

Be aware that these are running on the production server.
Here is a proposed order of steps, but you can send most of these requests independently of each other.

1. Send request `Get Access Token`. This provides you with access to the API.
2. Send request `Get sale unit details based on MSN`. This returns a JSON structure with the details, including the org number. If necessary, update `orgno` in the environment.
3. Send `Get merchant by organization number` for details about the transaction.
4. Open `Order products on behalf of merchants` to see an example of ordering products. Since this is running on the production server, you might not want to run it.

## Questions?

We're always happy to help with code or other questions you might have!
Please create an [issue](https://github.com/vippsas/vipps-partner-api/issues),
a [pull request](https://github.com/vippsas/vipps-partner-api/pulls),
or [contact us](https://github.com/vippsas/vipps-developers/blob/master/contact.md).

Sign up for our [Technical newsletter for developers](https://github.com/vippsas/vipps-developers/tree/master/newsletters).
