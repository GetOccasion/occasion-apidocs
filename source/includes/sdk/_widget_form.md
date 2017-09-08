# 6. Complete this form to book this product

```javascript
occsnClient.Order.construct({ product: window.product })
.then(function(order) {
  window.order = order;
});
```

Time to create the order form. How do we display an order form with all of its requirements, when those requirements may change depending on what product you are selling?

To answer this, the SDK provides
the function `Order.construct` shown in this example to initialize an order with the specifics required of the product it is selling. The exact functionality of the `construct` method will be covered in each of the remaining sections where it is relevant.

> The remainder of this guide will assume that you've set `window.order` equal to the constructed order for `window.product`.

## Tracking sessions

```javascript
console.log(window.order.sessionIdentifier)
// => "jo7xer-1504906476059"
```

`construct` instantiates each order with a `sessionIdentifier` that is unique. This session identifier is used by Occasion for different purposes related to tracking sessions.

You can use `sessionIdentifier` for your own application too.