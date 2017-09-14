# 10. Do you have a coupon or any gift cards you'd like to use?

You can provide customers with the ability to add a coupon or any number of gift cards to their order. This could be
implemented as a single text input that takes in a code, checks that it's valid, and then displays the coupon or gift
card information on the order widget, indicating that it has been added to the order while updating the order price.

## Finding coupons and gift cards by code

```javascript
window.product.redeemables().findBy({ code: 'HOLIDAYS45' })
.then(function(redeemable) {
  if(redeemable.isA(occsnClient.Coupon)) {
    
    console.log(redeemable.attributes()) // =>
    // {
    //   id: 'bh7ag0zn',
    //   code: 'HOLIDAYS45',
    //   name: 'Holiday Coupon',
    //   discount_fixed: '5.0',
    //   discount_percentage: null
    // }
    //
    // *or*
    //
    // {
    //   id: 'bh7ag0zn',
    //   code: 'HOLIDAYS45',
    //   name: 'Holiday Coupon',
    //   discount_fixed: null,
    //   discount_percentage: '10.0'
    // }
    
  } else if(redeemable.isA(occsnClient.GiftCard)) {
    
    console.log(redeemable.attributes()) // =>
    // {
    //   id: '56bvcf4e',
    //   code: 'HOLIDAYS45',
    //   initial_value: '50.0',
    //   value: '10.0'
    // }
  }
  
})
.catch(function(errors) {
  console.log(errors) // =>
  //
  // 404 Not Found
  //
  // {
  //   parameter: 'filter/code',
  //   code: 'notFound',
  //   detail: 'Could not find redeemable with code: "HOLIDAYS45"'
  // }
  //
  // *or*
  //
  // 409 Conflict
  //
  // {
  //   parameter: 'filter/code',
  //   code: 'unavailable',
  //   detail: 'A coupon or gift card was found, but is no longer available for use.'
  // }
})
```

> All possible error responses are displayed in the example

The relationship `product.redeemables()` enables you to search for any redeemables (coupon or gift card) that can be redeemed
for the product being ordered, using `findBy()` to find the distinct redeemable for the code the customer entered.

Every resource returned from a promise in the SDK has a function `isA(class)`, which will return true if the resource is an
instance of the `class` provided.

Once we've found a redeemable, we can use `isA` to see if it is an `occsnClient.Coupon`, or an `occsnClient.GiftCard`.

Coupons and gift cards will have different `attributes()`, as displayed in the example. These attributes are:

### Coupons

Attribute | Description
--------- | -----------
`code` | The coupon code
`name` | The name of the coupon
`discount_fixed` | The fixed monetary discount provided by the coupon. Will be `null` if `discount_percentage` exists.
`discount_percentage` | The percentage discount provided by the coupon. Will be `null` if `discount_fixed` exists.

### Gift Cards

Attribute | Description
--------- | -----------
`code` | The gift card code
`initial_value` | The initial value that was loaded onto the gift card.
`value` | The remaining value on the gift card that can be applied to the order.

## Adding the redeemable to the order

```javascript
window.product.redeemables().findBy({ code: 'HOLIDAYS45' })
.then(function(redeemable) {
  if(redeemable.isA(occsnClient.Coupon)) {
    // Assign the coupon to the order if the redeemable is a coupon
    window.order.assignCoupon(redeemable);
    
  } else if(redeemable.isA(occsnClient.GiftCard)) {
    // Charge gift card for its entire value if the redeemable is a gift card
    // @see Chapter 11 for more information on `charge`
    window.order.charge(redeemable, redeemable.value);
  }
})
```

Once we've found a redeemable, we check to see if it is an `occsnClient.Coupon`, and if it is, we `window.order.assignCoupon(coupon)`.

If it is a `occsnClient.GiftCard`, use `order.charge` to charge the gift card for the value specified in the second argument, in this case its entire `value`.

## Removing redeemables from the order

```javascript
// Remove coupon by setting order.coupon equal to null
window.order.assignCoupon(null);

// Remove gift card using order.removeCharge
window.order.removeCharge(giftCardToRemove);
```

You can easily remove redeemables using the functions displayed in this example.

## Updating order price

If we add a coupon or a gift card to the order, the price is going to change (unless it is already free, of course).

To reflect any discount provided by a redeemable, you should call the `window.afterPriceCalculatingItemChange` callback
created in Chapter 9 Section 2 after adding the redeemable to the order.

> Remember to bind the event for successfully finding a redeemable to update the order price using `afterPriceCalculatingItemChange`.
See Chapter 9 Section 2.