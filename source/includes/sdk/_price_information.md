# 12. Your total today is...

The last section of the order widget takes no input. Instead, it displays the result of a customer's choices: the subtotal, savings, tax, and total of the order.

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
    //   balance: '6.0'
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
`balance` | The remaining balance after `giftCardAmount` has been deducted from `price`.

You should display these attributes to the customer accordingly, so that they have a full understanding of exactly what charges they are receiving on their
payment method.

## The numbers must add up

In the previous chapter we made use of `order.balance` to charge the credit card provided for the "remaining balance"
left on the order.

**An order saved to Occasion is only valid if all of the charges add up to `order.price`, otherwise your order will fail to save.**

This is why it is so useful to wait until the order form has been submitted before processing the credit card data and
building/charging a `CreditCard`. You will know the final `order.balance` after the customer has finished answering questions and
adding all of their gift cards and coupons, rather than having to continually edit the credit card charge each time `balance` changes
with `price`.

The conclusion is simple: just charge credit cards for `order.balance` when the order form is submitted.
Let `updatePrice()` do the rest and the numbers will always add up.