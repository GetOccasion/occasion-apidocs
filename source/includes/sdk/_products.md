# 3. Browsing Merchants and Products

This chapter will set the foundation for building an order widget by demonstrating how to query merchants and their products, perhaps to provide customers with the ability to view all of a merchant's products before selecting one to book.

*It will also highlight the DSL for the SDK's query interface, so it is useful for you to read this chapter completely.*

## Getting All Merchants

```javascript
occsnClient.Merchant.all()
   .then(function(merchants) {
     merchants.each((merchant) => ...) // do something with each merchant
   });

```

If your API token permits you to access all of Occasion's merchants, you can use `Merchant.all()` to receive a promise for a `Collection` of all merchants, and then process each one individually when you receive them.

## Getting a Specific Merchant

```javascript

occsnClient.Merchant.find('712h3as')
  .then(function(merchant) {
    // do something with Merchant(id: '712h3as')
  })
  .catch(function(errors) {
    console.log(errors)
    // =>
    //  [
    //    {
    //      parameter: 'id',
    //      code: 'notFound',
    //      detail: 'Could not find merchant with id: "712h3as"'
    //    } 
    //  ]
  });
```

You can use `Merchant.find(id)` to load a specific merchant by ID. The promise returned will yield either a resource of class `Merchant` or errors.

## Getting Your Individual Merchant Account

```javascript
occsnClient.Merchant.first()
  .then(function(merchant) {
    // do something with your individual merchant
  });
```

If your API token is for a single merchant using Occasion, rather than an Occasion API partner, and you want to retrieve your merchant account's information, you can use `Merchant.first()`.

## Getting A Merchant's Venues and Products

```javascript
occsnClient.Merchant.find('712h3as')
  .then(function(merchant) {
    // do something with merchant
    
    // Retrieves merchant's venues from the server
    merchant.venues().all()
      .then(function(venues) {
        venues.each((venue) => ...) // do something with each venue
      });
    
    // Retrieves merchant's products from the server
    merchant.products().all()
      .then(function(products) {
        products.each((product) => ...) // do something with each product
      });
    
    // Loads merchant's venues from the server and saves them to
    // merchant.venues().target()
    merchant.venues().load()
      .then(function(venues) {
        venues.each((venue) => ...) // do something with each venue
      });
    
    // Retrieves merchant's product ID 'n2as78' from the server
    merchant.products().find('n2as78')
      .then(function(product) {
        // do something with Product(id: 'n2as78')
      })
      .catch(function(errors) {
        console.log(errors)
        // =>
        //  [
        //    {
        //      parameter: 'id',
        //      code: 'notFound',
        //      detail: 'Could not find product with id: "n2as78"'
        //    } 
        //  ]
      });
    
    // Retrieves merchant's first product from the server
    merchant.products().first()
      .then(function(product) {
        // do something with merchant's first product
      });
    
    // Retrieves merchant's last 3 products from the server
    merchant.products().last(3)
      .then(function(products) {
        products.each((product) => ...) // do something with each product
      });
  })
```

The Occasion SDK allows you to easily navigate any resource and any relationship of any resource with the exact same relational format. In the way that we retrieve all merchants or find a specific merchant by ID,
we can also retrieve all of a specific merchant's venues and products, as well as find a specific venue or product by ID amongst the merchant's.

*Note the difference between using `merchant.venues().all()` and `merchant.venues().load()`. The former retrieves the venues from the server and responds with them, the latter does the same but also stores them to `merchant.venues().target()`.*

You can also call `.first(n)` and `.last(n)` on any resource or relationship, as well as include any relationship 

## Eager Loading Venues and Products

```javascript
occsnClient.Merchant.includes({ venues: 'products' }).first()
  .then(function(merchant) {
    // show merchant, with pages for venues and each of
    // the venues' products (all already loaded)
    
    // get array of venues loaded to target()
    let venues = merchant.venues().target.all();
    
    // gets the first venue loaded to target()
    let venue = merchant.venues().target().first();
    
    // get the first venue's last product
    let product = venue.products().target().last();
    
    // true, because relationships are constructed between resources
    venue === product.venue();
  });
```

You can also make use of eager loading relationships by using `includes`. This will load any relationships along with the primary resource(s) you are retrieving, and allow you to explore local copies of all of these resources linked together seamlessly all in one query.

**It is not recommended you make this query on larger merchants because it could be slow responding with large numbers of venues and products. Instead, think consciously about where it makes sense to eager load vs. other methods.**

## Conclusion

This chapter demonstrates some of the DSL used to query resources in the Occasion SDK. To explore the entire interface for querying resources, see the Advanced Section under Querying and Relations.