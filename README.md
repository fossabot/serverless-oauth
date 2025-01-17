# @particular./serverless-oauth

[![npm version](https://img.shields.io/npm/v/@particular./serverless-oauth.svg)](https://www.npmjs.com/package/@particular./serverless-oauth) [![semantic-release](https://img.shields.io/badge/%20%20%F0%9F%93%A6%F0%9F%9A%80-semantic--release-e10079.svg)](https://github.com/semantic-release/semantic-release) [![code style: prettier](https://img.shields.io/badge/code_style-prettier-ff69b4.svg)](https://github.com/prettier/prettier) [![CircleCI](https://img.shields.io/circleci/project/github/uniquelyparticular/serverless-oauth.svg?label=circleci)](https://circleci.com/gh/uniquelyparticular/serverless-oauth)
![dependency status: david](https://img.shields.io/david/uniquelyparticular/serverless-oauth.svg)
[![FOSSA Status](https://app.fossa.io/api/projects/git%2Bgithub.com%2Funiquelyparticular%2Fserverless-oauth.svg?type=shield)](https://app.fossa.io/projects/git%2Bgithub.com%2Funiquelyparticular%2Fserverless-oauth?ref=badge_shield)

> 🎮 Minimal OAuth implementation using Serverless!

Built with [Micro](https://github.com/zeit/micro)! 🤩

## 🛠 Setup

Both a [Shopify](https://shopify.com) _and_ [Firebase](https://firebase.google.com) account are needed for this to function _(NOTE: this is only temporary)_.

Start ngrok (change ngrok port below from 3000 if going to run yarn dev on different port or if already in use)

```bash
ngrok http 3000
```

Make a note of the https `ngrok URL` provided.

---

Create a `.env` at the project root with the following credentials:

```dosini
DEPLOYED_URI
FIREBASE_PROJECT_ID
FIREBASE_CLIENT_ID
FIREBASE_PRIVATE_KEY_ID
FIREBASE_PRIVATE_KEY
SHOPIFY_OAUTH_SCOPES
SHOPIFY_API_KEY
SHOPIFY_API_SECRET
```

---

`DEPLOYED_URI` should be set to your `ngrok URL` from above (ie. `https://312a9670.ngrok.io`)

Open the [Firebase Console](https://console.firebase.google.com) to create a new Project (or you can use an existing one) to use for storing temporary nonce date. Click `Add Project`, enter anything in the `Project Name` field then click `Create Project`. When you receive the 'Your new project is ready' confirmation, click `Continue`.

Go into the `Settings` for your new project (click gear icon) and click on `Service Accounts` tab. Click the `Generate new private key` button to download a JSON file containing your Service Account credentials.

From that JSON file, copy the following to your env entries:
`project_id` >> `FIREBASE_PROJECT_ID`
`client_id` >> `FIREBASE_CLIENT_ID`
`private_key_id` >> `FIREBASE_PRIVATE_KEY_ID`

Grab the value of the key containing between `-----BEGIN PRIVATE KEY-----` and `-----END PRIVATE KEY-----\n` to set as the value of `FIREBASE_PRIVATE_KEY`
\*If deploying to Zeit Now instead of ngrok, make sure to replace `\n` in the string w/ `\\n` before storing as a secret.

---

`SHOPIFY_OAUTH_SCOPES` can be set to any of the following values: `read_products`,`read_product_listings`,`read_customers`,`write_customers`,`write_orders,write_draft_orders`,`write_shipping`,`write_checkouts`,`read_shopify_payments_disputes`,`unauthenticated_read_product_listings`,`unauthenticated_write_checkouts`,`unauthenticated_write_customers`.

Navigate to your [Shopify Partner Dashboard](https://partners.shopify.com/<<PartnerId>>/apps)'s App section and clicking `Create App`.

You can enter any value for `App Name`.

In the `App URL` field, be sure to enter your `ngrok URL` (provided above) followed by `/auth` such that `App URL` looks something like `https://312a9670.ngrok.io/auth`.

In the `Whitelisted redirection URL(s)` field, be sure to enter your `ngrok URL` (provided above) followed by `/auth/callback` such that `App URL` looks something like `https://312a9670.ngrok.io/auth/callback`.

Click the `Create app` button to create your App Credentials and find your `SHOPIFY_API_KEY` and `SHOPIFY_API_SECRET`.

## 📦 Package

Run the following command to build the app

```bash
yarn install
```

Start the development server

```bash
yarn dev
```

The server will typically start on PORT `3000`. If not, you'll need to restart ngrok to point to whatever server port you've started here.

## ⛽️ Usage

Once your server is up and running, navigate back to your [Shopify Partner Dashboard](https://partners.shopify.com/<<PartnerId>>/apps)'s App section and clicking on the App you installed above (if you're not still there).

Open the `Test your app` accordian button > Select a store from the dropdown > Click the `Install app on store` button and follow the prompts to confirm your installation and `Install Unlisted app`.

**_Make a note of the `access_token` provided as you will need it for making subsequent API calls._**

**NOTE**: this repository works extremely well with our `@particular./shopify-auth` package which is available via `npm` or at:
https://github.com/uniquelyparticular/shopify-request.

```js
const { createClient } = require('@particular./shopify-request');
// import { createClient } from '@particular./shopify-request'

const shopify = new createClient({
  store_name: '...', //Shopify Store Name
  access_token: access_token //Shopify OAuth token received after registering as Public App and installing to Store above
});
```

## 🚀 Deploy

You can easily deploy this function to [now](https://now.sh).

_Contact [Adam Grohs](https://www.linkedin.com/in/adamgrohs/) @ [Particular.](https://uniquelyparticular.com) for any questions._


## License
[![FOSSA Status](https://app.fossa.io/api/projects/git%2Bgithub.com%2Funiquelyparticular%2Fserverless-oauth.svg?type=large)](https://app.fossa.io/projects/git%2Bgithub.com%2Funiquelyparticular%2Fserverless-oauth?ref=badge_large)