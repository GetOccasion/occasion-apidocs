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

console.log(window.order.errors().forField('customer').toArray()); // =>
// [
//   {
//     field: "customer.firstName"
//     code: "blank"
//     detail: "Customer.First Name cannot be blank."
//   },
//   
//   {
//     field: "customer.lastName"
//     code: "blank"
//     detail: "Customer.Last Name cannot be blank."
//   },
//   
//   {
//     field: "customer.email"
//     code: "invalid"
//     detail: "Customer.Email is invalid."
//   }
// ]


console.log(window.order.errors().detailsForField('timeSlots')); // =>
// {
//   blank: "Orders for product id: '94hn_pte' require at least one time slot."
// }


console.log(window.order.errors().forField('answers').toArray()); // =>
// [
//   {
//     field: "answers.option"
//     code: "blank"
//     detail: "Answer option cannot be blank."
//   },
//
//   {
//     field: "answers.value"
//     code: "invalid"
//     detail: "Answer value is invalid."
//   }
// ]


console.log(window.order.errors().forField('coupon').toArray()); // =>
// [
//   {
//     field: "coupon"
//     code: "invalid"
//     detail: "Coupon is invalid."
//   },
//
//   {
//     field: "coupon"
//     code: "inactive"
//     detail: "Coupon is inactive at this time."
//   },
//
//   {
//     field: "coupon"
//     code: "depleted"
//     detail: "Coupon is no longer available."
//   }
// ]


console.log(window.order.errors().forField('transactions').toArray()); // =>
// [
//   {
//     field: "transactions.amount"
//     code: "invalid"
//     detail: "Transactions.Amount is invalid."
//   },
//   
//   {
//     field: "transactions.paymentMethod"
//     code: "blank"
//     detail: "Transactions.Payment Method cannot be blank."
//   },
//   
//   {
//     field: "transactions.paymentMethod"
//     code: "declined"
//     detail: "Transactions.Payment Method declined."
//   }
// ]

console.log(window.order.errors().forBase().toArray()); // =>
// []
```

> All possible errors are shown in this example.

An efficient error display will let the customer know what mistakes they've made on the form or what errors have occurred in processing
the order.

You can get a collection of all of the errors for a given attribute or relationship using `errors().forField(name)`. You can
also use `errors().detailsForField(name)` for an object that summarizes the errors. These are useful for displaying errors next to the input(s)
that generated them.

You can get all of the errors that are associated with the base `order` (rather than a specific field) using `errors.forBase()`.