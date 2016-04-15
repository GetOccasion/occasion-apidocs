---
title: Occasion API Documentation

language_tabs:
  - shell

toc_footers:
  - <a href='https://app.getoccasion.com/users/sign_up'>Sign Up for an Account</a>
  - <a href='https://github.com/tripit/slate'>Documentation Powered by Slate</a>

includes:
  - query
  - merchant
  - products
  - errors

search: true
---

# Introduction

Welcome to the Occasion API! You can use our API to access Occasion API endpoints, which can be used to interact with all levels of functionality available to Occasion users, including: products, venues, orders, coupons, gift cards, customers, payment methods, users, calendars, etc.

**Right now, the only endpoints available for query are products. However, we are rapidly expanding to include all other endpoints.**

We have planned language bindings in Shell, Ruby, and Javascript! You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.

**Right now, query can only be made via Shell (cURL, etc.), but we plan on releasing a Javascript library followed by Ruby.**

# Format

All responses are in JSON. All requests should be made in JSON as well. In the future, we will force requests to be in JSON format, otherwise `415 Unsupported Media Type`

# Authentication

> To authorize, use this code:

```shell
# With cURL, you can make use of the -u option to create a basic authentication header
curl "api_endpoint_here"
  -u "[API_LOGIN]:[API_SECRET]"
```

> Make sure to insert your own API login and secret keys.

Unless otherwise noted, all calls to Occasion API use [HTTP basic authentication](https://en.wikipedia.org/wiki/Basic_access_authentication) over HTTPS.

Basic authentication requires a login key and a secret key. You can find your API keys on your [account page](https://app.getoccasion.com/users/edit). You must be signed into your account to view this page.

Occasion requires that at the very least your API login key be provided with all queries made to our servers. Some endpoints are public, and only require an API login key. Others are private, and require that your API secret key be provided as well. Unless noted otherwise, all endpoints are public.

The data that an endpoint responds with may vary depending of whether or not a secret key was provided. For example, making a public call to `GET /products` will respond with a list of all your products, but any sensitive information will not be included. Making a private call (the secret key included) to the same endpoint will respond with all of your products, with all their information included. This allows you to use the API in a public environment without having to worry about any sensitive data being compromised. The difference between response bodies will be noted in the information regarding each endpoint.
