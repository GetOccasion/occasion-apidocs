# 7. What is your contact information?

## Guest Checkout

```javascript
window.order.customer().attributes() // =>
// {
//   email: null,
//   firstName: null,
//   lastName: null,
//   zip: null
// }
```

The first part of the order form is to ask the customer for their email, first name, last name, and zip code. `Order.construct` will build a blank customer for you. Bind each of the customer's attributes to form inputs using your frontend library of choice.

This is called "Guest Checkout," because it enables a customer to book any product without signing into any account, enabling faster purchase.

## Account Sign In

```javascript
occsnClient.Customer.signIn({
  email: 'customer@example.com',
  password: '********'
})
  .then(function(existingCustomer) {
    
    // Replace the guest customer with the existing customer
    window.order.assignCustomer(existingCustomer);
  })
  .catch(function(errors) {
    console.log(errors) // =>
    //  [
    //    {
    //      parameter: 'email',
    //      code: 'notFound',
    //      detail: 'Could not find customer with email: "customer@example.com"'
    //    },
    //    {
    //      parameter: 'email',
    //      code: 'unconfirmed',
    //      detail: 'We need to verify your email address first. Please check your inbox and verify your email address.'
    //    },
    //    {
    //      parameter: 'password',
    //      code: 'invalid',
    //      detail: 'Incorrect password'
    //    },
    //  ]
  });
```

> All possible errors of this method are displayed in the example.

You can also allow customers to sign into accounts that are persisted in Occasion's database, all they have to do is enter their email and password. Display a sign in form somewhere on your page and when the form is submitted, call `Customer.signIn`.

*A customer can choose to save their account information on completion of purchase, which we will cover in the next section.*

## Account Creation

Coming soon...