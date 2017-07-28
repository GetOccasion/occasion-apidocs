# 14. Thanks...*or*...There was a problem

After the order form is submitted, your customer will either achieve great success, or experience crushing failure.

To make this experience best, give them a great thank you page, and an effective error display.

## Success

```javascript
console.log(window.product.postTransactionalMessage); // =>
// Thanks for booking our product!

// Attributes after the order is saved to the server
console.log(window.order.attributes()); // =>
// {
//   id: '875ahny6',
//   verificationCode: 'kASn37a',
//   status: 'booked',
//   createdAt: '2015-10-23T11:00:44.539-05:00',
//   updatedAt: '2015-10-23T11:00:44.539-05:00',
//   tax: '0.0',
//   taxPercentage: '0.0',
//   couponAmount: '1.0',
//   couponDescription: '$1.00',
//   price: '10.0',
//   quantity: 1,
//   description: 'The title of the product being ordered.'
// }
```

Displaying a success screen to the customer is simple. Do away with the order form, and show them `product.postTransactionalMessage`.

You can also choose to show them any of the `attributes()` of the saved order, the output of which is shown in this example.

## Error

```javascript
// Errors after the order fails to save to the server

console.log(window.order.errors().forField('customer')); // =>
// [
//   {
//   },
// ]

console.log(window.order.errors().forField('timeSlots')); // =>
// [
//   {
//   },
// ]

console.log(window.order.errors().forField('answers')); // =>
// [
//   {
//   },
// ]

console.log(window.order.errors().forField('coupon')); // =>
// [
//   {
//   },
// ]

console.log(window.order.errors().forField('transactions')); // =>
// [
//   {
//   },
// ]

console.log(window.order.errors().forBase()); // =>
// [
//   {
//   },
// ]
```

> All possible errors are shown in this example.

**TODO: Display possible errors for `order.save`**

An efficient error display will let the customer know what mistakes they've made on the form or what errors have occurred in processing
the order.

You can get all of the errors for a given attribute or relationship using `errors().forField(name)`. This is useful for displaying errors next to the input(s)
that generated them.

You can get all of the errors that are associated with the base `order` (rather than a specific field) using `errors.forBase()`. You could
display those at the bottom of the order widget or wherever works best for you.