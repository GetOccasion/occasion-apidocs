# 4. Laying Out The Widget For a Product

Once your customer has selected a product to be purchased, you should show them a widget / form to create an order for that product. The remaining chapters will demonstrate how to create such a form, with this section dedicated to outlining the basic structure and components of a widget.

**A great widget will provide the customer with a booking experience similar to a conversation. All of the chapters that come after this one will be structured like such a conversation, with the merchant speaking to the customer and the customer responding with user interaction.**

## But first, load the product with relevant data

> This example shows the basic gist of the structure of an order widget, where each comment represents a section of the HTML form. The product can customize the title that comes before each section. The remaining chapters of this guide assume you display these titles as you see fit, and will show you how to implement the `@todo` of each section.

```javascript
let productId = 'ashw762j';

occsnClient.Product.includes('merchant', 'venue').find(productId)
  .then(function(product) {
    // do something with the product, with its merchant and venue loaded
    
    window.product = product;
    console.log(product.title);
    console.log(product.venue().attributes());
     
    //
    // Header
    //
    
    console.log(product.title);
    // --------------------------
    // @todo Implement Chapter 5
    // --------------------------
    
    //
    // Order Form
    //
    
    // --------------------------
    // @todo Implement Chapter 6
    // --------------------------
    
      //
      // Contact Information
      //
      
      console.log(product.widgetContactsTitle);
      // --------------------------
      // @todo Implement Chapter 7
      // --------------------------
      
      //
      // Time Slot Information
      //
      
      console.log(product.widgetTimeSlotsTitle);
      // --------------------------
      // @todo Implement Chapter 8
      // --------------------------
      
      //
      // Additional Questions
      //
      
      console.log(product.widgetQuestionsTitle);
      // --------------------------
      // @todo Implement Chapter 9
      // --------------------------
      
      //
      // Coupon and Gift Card Redemption
      //
      
      // --------------------------
      // @todo Implement Chapter 10
      // --------------------------
      
      //
      // Payment Information
      //
      
      console.log(product.widgetsPaymentTitle);
      // --------------------------
      // @todo Implement Chapter 11
      // --------------------------
      
      //
      // Price Information
      //
      
      console.log(product.widgetsTotalDueTitle);
      // --------------------------
      // @todo Implement Chapter 12
      // --------------------------
      
      //
      // Submit Order Button
      //
      
      // --------------------------
      // @todo Implement Chapter 13
      // --------------------------
      
      //
      // After Submit (Success, Errors)
      //
      
      // --------------------------
      // @todo Implement Chapter 14
      // --------------------------
  });
```

Assuming you only know the ID of the product you want to load, you can use `Product.find(id)` to retrieve the product you want to sell,
including its `merchant` and `venue` so you can display their information too.

You can then access any attribute of any resource as if it were a normal property of a Javascript object. **Relationships are always defined as functions, rather than properties.**

Using the function `attributes()`, you can quickly get an `Object` of useful information for each resource. We've limited the output in each example to relevant attributes only.

> The remainder of this guide will assume that you've set `window.product` equal to the loaded product that you are selling.

## Always make sure you are selling an active product

```javascript
switch(window.product.status) {
  case 'active':
    // display order widget
  case 'inactive':
    // not accepting orders
  case 'expired':
    // has time slots, but all have passed
  case 'sold_out':
    // fully booked
}
```

A product can have four statuses. Customers can only book `active` products, so you should always check that a product is `active` before allowing someone to book it.

*You could also limit the products you display for browsing to those you know a customer can book. See this in the Advanced Section, under Querying and Relations.*

<br/><br/>
**With that, let's start the conversation...**