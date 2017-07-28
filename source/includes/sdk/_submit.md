# 13. Submit your order

The time has come. We are now ready to add the big "Finalize order" button at the bottom of the widget.

## The button

```javascript
window.product.orderButtonText
```

When displaying this big beautiful button in all its glory, make sure to do it the way our merchants want!

The product has `orderButtonText` to shine the way.

## Finallyze

```javascript
window.order.save(function() {
  if(window.order.persisted()) {
    // order was a success, go to the completion page
  } else {
    // order failed for some reason, read the errors
    
    console.log(window.order.errors().toArray()) // =>
    // @see Chapter 14 Section 2
  }
});
```

You can attempt to persist any resource in the SDK at any time by calling `save(callback)` on it.

When `save` receives a response, the `callback` will execute regardless of whether or not the
attempt was a success or failure, and you can call the original `window.order` from the `callback` because `save` mutates
the original object it was called on rather than responding with a new one.

`persisted()` indicates whether or not any resource in the SDK exists on our server. If an order fails to save, it will
not be persisted on our server.

Instead, it will have `errors()` that you can display for the customer, which will be shown in the next chapter.