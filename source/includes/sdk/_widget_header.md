# 5. Hi! Let me tell you about who we are, what this product offers you, and where we're located

```javascript
console.log(window.product.merchant().name); // Chicago's Art Studio

console.log(window.product.merchant().attributes()); // =>
// {
//   name: 'Chicago\'s Art Studio',
//   profilePicture: 'https://s3.amazonaws.com/development.assets.playoccasion/uploads/profile.jpg',
//   timeZone: 'America/Chicago',
//   facebookPage: 'https://www.facebook.com/xxxxxxx'
// }
 
console.log(window.product.attributes()); // =>
// {
//   title: 'Paint Party',
//   description: 'You are here to paint, and you are here to party',
//   image: {
//     url: 'https://s3.amazonaws.com/development.assets.playoccasion/uploads/product/image/xxxxx/xxxxx.jpg',
//     thumb: {
//       url: 'https://s3.amazonaws.com/development.assets.playoccasion/uploads/product/image/xxxxx/xxxxx.jpg'
//     }
//   },
//   status: 'active',
//   taxPercentage: '3.5'
// }
 
console.log(window.product.venue().attributes()); // =>
// {
//   name: 'Lakeview Campus',
//   address: '123 Main Street',
//   city: 'Chicago',
//   website: 'www.example.com',
//   email: 'admin@example.com',
//   phone: '(999) 999-9999',
//   timeZone: 'America/Chicago'
// }
```

The header of the widget is about introducing the customer to the merchant and the product they're selling.

Use any of the snippets or properties in this example to display relevant product, venue, and merchant information in the order widget.