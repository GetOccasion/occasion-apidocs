# 12. Please enter your payment information

```javascript
window.merchant.pspName // => 'cash'
```

After the customer has selected any coupons or gift cards, it is time for them to enter their payment information.
Right now only cash and credit cards are supported, but other platforms may be featured in future releases.

Each merchant on Occasion accepts payments using a payment service provider (PSP): Cash, Spreedly, or Square, and they can only use one. The latter two process credit cards. The following
sections will show you how to handle each individual case.

First off, though, you must determine which PSP the merchant uses. To do this, read the `merchant.pspName` attribute, as shown in the example.
Possible names include:

PSP | Name
---- | -------
Cash | `cash`
Spreedly | `spreedly`
Square | `square`

## Accept cash only

For merchants with `pspName == 'Cash'`, payment for an order is collected in cash when the customer
comes in for their reservation. For these merchants, no additional
measures must be taken to collect payment information to use to pay for the order.

## Build and charge a credit card using a payment processor payment method token

Occasion does not process payment information through our own application, we use PCI compliant 
payment processing services to do this for us, and there are two options. Each provider offers an iFrame script that can
used to securely send credit card information to their server, and receive a token back that Occasion uses to process
payment for the order.

### Spreedly

```javascript
Spreedly.init('UnQhm0g7l3nOIz2hmAoV3eqm26k',
  {} // ... additional config required, see Spreedly docs
);

window.onOrderFormSubmit = function(e) {
  var creditCardData = {
    // see documentation
  };
  
  Spreedly.tokenizeCreditCard(creditCardData)
  
  Spreedly.on('paymentMethod', function(token) {
    var creditCard = occsnClient.CreditCard.build({ id: token });
    
    window.order.charge(creditCard, window.order.outstandingBalance);
    
    // @todo Implement Chapter 13
    // window.order.save
  });
  
  Spreedly.on('errors', function(errors) {
    // do something with errors
  });
};
```

[Spreedly](https://www.spreedly.com/) supports hundreds of payment gateway services like Stripe, Braintree, Authorize.net, and more.
**Note:** At this time, Paypal support through Spreedly is not enabled in the Occasion SDK, though a future release will add support.

To add a Spreedly payment form to your application, we suggest using their iFrame payment method script, which you can find a guide
on [here](https://docs.spreedly.com/guides/adding-payment-methods/iframe/).

The example shows a simplified version of the basic steps you'll have to take to implement this form in your application once the script has been added:

1. Initialize Spreedly using Occasion's Spreedly environment key
2. Create a payment method token from user-input credit card information once the order form is submitted
3. Submit order to Occasion with the payment method token using the Occasion SDK

Use our environment key with the Spreedly form:

Name | API Key
--------- |  -----------
**Spreedly** | `UnQhm0g7l3nOIz2hmAoV3eqm26k`

### Square

```javascript
window.squareForm = new SqPaymentForm({
    applicationId: "sq0idp-kKdgouNdlT2lj08V0tSJ3g",
    // ... additional config required, see Square docs
    callbacks: {
      cardNonceResponseReceived: function(errors, nonce) {
        if(errors) {
          // do something with errors
        } else {
          var creditCard = occsnClient.CreditCard.build({ id: nonce });
              
          window.order.charge(creditCard, window.order.outstandingBalance);
          
          // @todo Implement Chapter 13
          // window.order.save
        }
      }
    }
});

window.onOrderFormSubmit = function(e) {
  window.squareForm.requestCardNonce();
};
```

[Square](https://squareup.com/) is a payment gateway much like the hundreds supported under Spreedly, but their closed platform must be implemented
individually.

To add a Square payment form to your application, we suggest using their iFrame payment method script, which you can find a guide
on [here](https://docs.connect.squareup.com/articles/adding-payment-form).

The example shows a simplified version of the basic steps you'll have to take to implement this form in your application once the script has been added:

1. Initialize Square using Occasion's Square application ID
2. Request a payment method nonce from user-input credit card information once the order form is submitted
3. Submit order to Occasion with the payment method nonce using the Occasion SDK

Use our key with the Square form:

Name | Application ID
--------- |  -----------
**Square** | `sq0idp-kKdgouNdlT2lj08V0tSJ3g`

## Edit or remove a credit card charge

```javascript
// Update the amount charged to the specified credit card to 9.0
window.order.editCharge(chargedCreditCard, 9.0);

// Remove the charged credit card from the order
window.order.removeCharge(invalidCreditCard);
```

If your order fails to save because the customer's credit card information was wrong, they're going to have to enter new credit card data.

But just because the order doesn't save doesn't mean the credit card is removed from it, the invalid credit card will remain on the order
even if you call `order.charge()` with a new credit card. **An order can only charge one credit card, valid or not valid.**

To prevent this scenario, you should remove invalid credit cards if they cause an order not to save, and then go through the process outlined
in the previous section in order to build a new credit card. 

If for any reason you need to edit the amount charged to any item that has already been charged, you can do that too.