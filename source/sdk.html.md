---
title: Occasion Javascript SDK Getting Started Guide

language_tabs:
  - javascript
  - json

toc_footers:
  - <a href='https://app.getoccasion.com/users/sign_up'>Sign Up for an Account</a>
  - <a href='https://github.com/tripit/slate'>Documentation Powered by Slate</a>

includes:
  - sdk/initialization
  - sdk/products
  - sdk/widget_structure
  - sdk/widget_header
  - sdk/widget_form
  - sdk/customer_information
  - sdk/time_slots_information
  - sdk/additional_questions
  - sdk/redeemables
  - sdk/payment_information
  - sdk/price_information
  - sdk/submit
  - sdk/after_submit
  - sdk/conclusion

search: true
---

# 0. Introduction

## Occasion Javascript SDK Getting Start Guide

The Occasion Javascript SDK enables you to sell bookings simply and securely through your web application, providing services to help you make use of many of the resources of Occasion. Such resources include merchants, products, venues, customers, orders, coupons, gift cards, payment methods, and calendars.

This guide will show you how to easily create a fully functioning order widget for booking products in your application. Every merchant in Occasion operates venues, and each venue has many products that it sells. Customers can buy these products through the order widget you will build today.

The process lets your customer browse products, select one for purchase, enter their personal information (or sign in to load their saved information), select one or more time slots,
answer any number of questions relevant to the product, include a coupon or any number of gift cards, as well as enter credit card information through our PCI compliant interface.

There is also an advanced section at the end that demonstrates how to make full use of the SDK's underlying technology to customize your application.

# 1. Installation

```javascript
npm i occasion-sdk --save
```

We use NPM to distribute our SDK. Use the command at right to download and save it to your `package.json`

You can also use the CDN address [https://unpkg.com/occasion-sdk](https://unpkg.com/occasion-sdk) to add it to your AMD loader or into your page:

`<script type='text/javascript' src='https://unpkg.com/occasion-sdk'></script>`