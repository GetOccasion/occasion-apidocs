# 11. Enter your payment information

After the customer has selected any coupons or gift cards, it is time for them to enter their payment information. Right now only credit
cards are supported, but Paypal and other platforms may be featured in future releases.

## Build and charge a credit card using a payment processor payment method token

```javascript
window.onOrderFormSubmit = function(e) {
  THIRD_PARTY_FUNCTION_TO_CREATE_PAYMENT_METHOD_TOKEN
  .then(function(token) {
    var creditCard = occsnClient.CreditCard.build({ id: token });
    
    window.order.charge(creditCard, window.order.outstandingBalance);
    
    // @todo Implement Chapter 13
  })
  .catch(function(thirdPartyErrors) {
    // do something with thirdPartyErrors on your own
  });
};
```

Occasion does not interpret or store payment information in our application, we outsource PCI compliance to our
payment processor services [Spreedly](https://docs.spreedly.com/guides/adding-payment-methods/javascript/)
and Payline Data.

You submit the credit card data to them alone and they'll tell you if it's valid. Then they'll give you a secure token for Occasion to process payment with on our server.

The steps involved in checking the validity of a credit card and safely charging it are as follows:

1. Use Spreedly or Payline's JS libraries to create a credit card form in the order widget. **The fields of these inputs will not be bound to any attribute or relationship of
`window.order`, because we do not want to submit this sensitive information to Occasion, only to the payment processor.**
2. Add a callback to the submit event of the overall `window.order` widget form *(not the credit card form)*.
3. When the submit callback is executed, send the credit card data to the payment processor. The payment processor will provide a function or endpoint that allows you to send credit card data to their server and receive in return
a payment method token corresponding to the cached payment method on their server.
4. Use this payment method token to build a `CreditCard` and charge it for the remaining balance of the order. Chapter 12 will explain `order.outstandingBalance` in more detail.
5. Carry through with the original submit event that was fired, and save the order to the server. See Chapter 13 for implementation.

**TODO: INFORMATION ON USING OCCASION'S ENV KEYS**

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