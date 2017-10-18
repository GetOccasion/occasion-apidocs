# 11. Your total today is...

Displaying the result of a customer's choices on the price of their order in real time is important to the experience. The special method `order.calculatePrice()`
can give you the subtotal, coupon discount, tax, and total price of the order.

It can also calculate the contribution of gift cards toward
the order's outstanding balance, to be paid using the payment method information collected in the next chapter.

## Displaying useful price information

```javascript
window.afterPriceCalculatingItemChange = function() {
  // called after the answer on `window.order` has already
  // been updated to reflect the new option or value specified
  // in the DOM
  
  window.order.calculatePrice()
  .then(function(order) {
    console.log(window.order.attributes()) // =>
    // {
    //   subtotal: '10.0',
    //   couponAmount: '1.0',
    //   tax: '2.0',
    //   giftCardAmount: '5.0',
    //   price: '11.0',
    //   outstandingBalance: '6.0'
    // }
  });
};
```

Every time:

* The answer to a `priceCalculating` question changes
* A coupon is added
* Gift cards are added

You must update the price displayed on the order widget
so the customer can see real-time how their choices affect the order's price. We've already covered in previous sections how to bind this callback appropriately - now we will explain how to
implement the remaining functionality.

Each time the `window.afterPriceCalculatingItemChange` callback shown is executed, it will call `window.order.calculatePrice()`,
which will automatically update `window.order` to have the following attributes:

Attribute | Description
--------- |  -----------
`subtotal` | The price of the order before coupon discount and tax have been added
`couponAmount` | The monetary value of the coupon that may have been applied to the order. If there is no coupon, this will equal `null`
`tax` | The monetary value of `product.tax_percentage` applied to `order.subtotal - order.couponAmount`
`giftCardAmount` | The monetary value of all of the gift cards charged to the order. If no gift cards, this will equal `null`.
`price` | The total price of the order after tax has been applied to the subtotal - discounts
`outstandingBalance` | The remaining balance after `giftCardAmount` has been deducted from `price`. Other payment methods like credit cards will have to pay this amount for the order to be completed paid for.

You should display these attributes to the customer accordingly, so that they have a full understanding of exactly what charges they are receiving on their
payment method.

## The numbers must add up

In the next chapter we will make use of `order.outstandingBalance` to charge a credit card for the remaining balance
left on the order.

**An order with payment methods (credit cards and gift cards), saved to Occasion, is only valid if all of the charges
to those payment methods add up to `order.price`, otherwise your order will fail to save.**

Note, this does not apply to orders that are paid for using cash, since no charges are created with that type of order.