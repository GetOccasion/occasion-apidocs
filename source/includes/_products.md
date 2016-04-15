# Products

## Get All Products

> **Private call** | Example truncated for brevity.

```shell
curl "http://app.getoccasion.com/api/v1/products"
  -u "59a8517fd9458b46d4ee59f8fd717fb80d:de7b7ae9e2e9e01a9508290e599"
```

```http
HTTPS/1.1 200 OK
```

```json
[
  {
    "id": 1,
    "merchant_id": 10,
    "venue_id": 15,
    "image": {
      "url": "https://s3.amazonaws.com/development.assets.playoccasion/uploads/product/image/xxxxx/xxxxx.jpg",
      "thumb": {
        "url": "https://s3.amazonaws.com/development.assets.playoccasion/uploads/product/image/xxxxx/xxxxx.jpg"
      }
    },
    "title": "My Art Class",
    "description": "Sign up to paint a teapot.",
    "order_button_text": "Finalize order",
    "status": "active",
    "created_at": "2015-10-23T11:00:44.539-05:00",
    "updated_at": "2015-10-23T11:00:44.539-05:00",
    "token": "38asnd2",
    "post_transactional_message": "Thank you for ordering.",
    "price": "10.0",
    "time_slots_closed_before": "2000-01-01T00:00:00.000Z",
    "embed_button_text": "Book now",
    "show_occurrence_availability": true,
    "tax_percentage": "2.0",
    "widget_contact_title": "Customer Information",
    "widget_occurrences_title": "Select which day you would like to reserve",
    "widget_attributes_title": "Additional Questions",
    "widget_payment_title": "Payment Information",
    "widget_total_due_title": "Total Due Today",
    "template_id": 8195,
    "capacity": 12,
    "show_time_slot_duration": false,
    "sells_gift_cards": false,
    "widget_gift_card_recipient_title": "Gift Card Recipient",
    "gift_card_redemption_message": "To redeem your gift card, visit our website.",
    "from_name": "My Business Name",
    "email_subject": "Thanks for ordering our product!",
    "url": "http://occ.sn/p/n/sdj291"
  }
]
```

> **Public call** | Example truncated for brevity.

```shell
curl "http://app.getoccasion.com/api/v1/products"
  -u "59a8517fd9458b46d4ee59f8fd717fb80d:"
```

```http
HTTPS/1.1 200 OK
```

```json
[
  {
    "image": {
      "url": "https://s3.amazonaws.com/development.assets.playoccasion/uploads/product/image/xxxxx/xxxxx.jpg",
      "thumb": {
        "url": "https://s3.amazonaws.com/development.assets.playoccasion/uploads/product/image/xxxxx/xxxxx.jpg"
      }
    },
    "title": "My Art Class",
    "description": "Sign up to paint a teapot.",
    "order_button_text": "Finalize order",
    "status": "active",
    "post_transactional_message": "Thank you for ordering.",
    "price": "10.0",
    "time_slots_closed_before": "2000-01-01T00:00:00.000Z",
    "embed_button_text": "Book now",
    "show_occurrence_availability": true,
    "tax_percentage": "2.0",
    "widget_contact_title": "Customer Information",
    "widget_occurrences_title": "Select which day you would like to reserve",
    "widget_attributes_title": "Additional Questions",
    "widget_payment_title": "Payment Information",
    "widget_total_due_title": "Total Due Today",
    "show_time_slot_duration": false,
    "sells_gift_cards": false,
    "widget_gift_card_recipient_title": "Gift Card Recipient",
    "url": "http://occ.sn/p/n/sdj291"
  }
]
```

This endpoint retrieves all products.

### HTTP Request

`GET http://example.com/api/v1/products`

### Response Body

Notable response fields include:

Field | Public | Description
----- | ------ | -----------
image | true | URLs for the full image and thumbnail to display with a product
title | true | The title of the product, such as "BYOB & Paint A Forest"
description | true | The description for the product, explaining things in detail
order_button_text | true | The text to display in the submit order button on an order widget
status | true | The status that will determine if the product is active for ordering.<br><br>*Possible values:*<br>**active:** Ready to accept orders<br>**inactive:** Not accepting orders<br>**expired:** Product has time slots, but none of them are open.<br>**sold_out:** Either product or all open time slots are fully booked
token | false | The token uniquely identifying a product on Occasion, in place of ID. **Cannot be used in place of ID in calls, yet, unless as** `GET /products?token=[token]`
post_transactional_message | true | The message to display after an order has been completed
price | true | The base price of the order, before applying price changing questions, tax, coupons, gift cards, etc.
time_slots_closed_before | true | The point in time before which time slots are closed for sales. Any time slot occurring between Time.now and the actual occurrence of that time slot (when the class takes place) cannot be sold.
embed_button_text | true | The text to display in an embed button that opens an order widget
show_occurrence_availability | true | If `true`, show how many open seats there are for a time slot
tax_percentage | true | The sales tax percentage that is applied to the subtotal of an order for this product
widget_contact_title | true | The title to display above a section regarding customer contact information (email, first_name, last_name, zip)
widget_occurrences_title | true | The title to display above a section regarding choosing a time slot
widget_attributes_title | true | The title to display above a section asking additional questions based off custom attributes
widget_payment_title | true | The title to display above a section asking for payment information like credit card details
widget_total_due_title | true | The title to display above a section indicating the total price of the order
widget_gift_card_recipient_title | true | The title to display above a section asking for the details of a gift card recipient (name, email, personal message), if the product `sells_gift_cards`
template_id | false | The ID of the template product that this product has been duplicated from
capacity | false | The amount of orders that can be reserved (booked but having not occurred yet) for a product
show_time_slot_duration | true | If `true`, display the duration of a time slot
sells_gift_cards | true | If `true`, display the gift card attributes in an order widget and create a gift card with the order, with a value equal to the total price of the order
gift_card_redemption_message | false | The message to display in additional to a gift card's personal message, typically instructing a recipient on how to redeem their gift card
from_name | false | The `from` name on the email sent to a customer after they complete an order
email_subject | false | The `subject` line on the email sent to a customer after they complete an order
url | true | The short URL to send someone to to purchase an order for a product

### Associations

Possible associations to include are:

Association | Default | Public | Description
----------- | ------- | ------ | -----------
merchant | false | true | The merchant that the product belongs to
venue | false | true | The venue that the product belongs to

## Get a Specific Product

> **Private call**

```shell
curl "http://app.getoccasion.com/api/v1/products/12"
 -u "59a8517fd9458b46d4ee59f8fd717fb80d:de7b7ae9e2e9e01a9508290e599"
```

```http
HTTPS/1.1 200 OK
```

```json
{
 "id": 12,
 "merchant_id": 10,
 "venue_id": 15,
 "image": {
   "url": "https://s3.amazonaws.com/development.assets.playoccasion/uploads/product/image/xxxxx/xxxxx.jpg",
   "thumb": {
     "url": "https://s3.amazonaws.com/development.assets.playoccasion/uploads/product/image/xxxxx/xxxxx.jpg"
   }
 },
 "title": "My Art Class",
 "description": "Sign up to paint a teapot.",
 "order_button_text": "Finalize order",
 "status": "active",
 "created_at": "2015-10-23T11:00:44.539-05:00",
 "updated_at": "2015-10-23T11:00:44.539-05:00",
 "token": "38asnd2",
 "post_transactional_message": "Thank you for ordering.",
 "price": "10.0",
 "time_slots_closed_before": "2000-01-01T00:00:00.000Z",
 "embed_button_text": "Book now",
 "show_occurrence_availability": true,
 "tax_percentage": "2.0",
 "widget_contact_title": "Customer Information",
 "widget_occurrences_title": "Select which day you would like to reserve",
 "widget_attributes_title": "Additional Questions",
 "widget_payment_title": "Payment Information",
 "widget_total_due_title": "Total Due Today",
 "template_id": 8195,
 "capacity": 12,
 "show_time_slot_duration": false,
 "sells_gift_cards": false,
 "widget_gift_card_recipient_title": "Gift Card Recipient",
 "gift_card_redemption_message": "To redeem your gift card, visit our website.",
 "from_name": "My Business Name",
 "email_subject": "Thanks for ordering our product!",
 "url": "http://occ.sn/p/n/sdj291"
}
```

> **Public call**

```shell
curl "http://app.getoccasion.com/api/v1/products/12"
 -u "59a8517fd9458b46d4ee59f8fd717fb80d:"
```

```http
HTTPS/1.1 200 OK
```

```json
{
 "image": {
   "url": "https://s3.amazonaws.com/development.assets.playoccasion/uploads/product/image/xxxxx/xxxxx.jpg",
   "thumb": {
     "url": "https://s3.amazonaws.com/development.assets.playoccasion/uploads/product/image/xxxxx/xxxxx.jpg"
   }
 },
 "title": "My Art Class",
 "description": "Sign up to paint a teapot.",
 "order_button_text": "Finalize order",
 "status": "active",
 "post_transactional_message": "Thank you for ordering.",
 "price": "10.0",
 "time_slots_closed_before": "2000-01-01T00:00:00.000Z",
 "embed_button_text": "Book now",
 "show_occurrence_availability": true,
 "tax_percentage": "2.0",
 "widget_contact_title": "Customer Information",
 "widget_occurrences_title": "Select which day you would like to reserve",
 "widget_attributes_title": "Additional Questions",
 "widget_payment_title": "Payment Information",
 "widget_total_due_title": "Total Due Today",
 "show_time_slot_duration": false,
 "sells_gift_cards": false,
 "widget_gift_card_recipient_title": "Gift Card Recipient",
 "url": "http://occ.sn/p/n/sdj291"
}
```

This endpoint retrieves a specific product.

### HTTP Request

`GET http://example.com/api/v1/products/:id`

### URL Parameters

Parameter | Description
--------- | -----------
id | The ID of the product to retrieve

### Response Body

Notable response elements include:

Field | Public | Description
----- | ------ | -----------
image | true | URLs for the full image and thumbnail to display with a product
title | true | The title of the product, such as "BYOB & Paint A Forest"
description | true | The description for the product, explaining things in detail
order_button_text | true | The text to display in the submit order button on an order widget
status | true | The status that will determine if the product is active for ordering.<br><br>*Possible values:*<br>**active:** Ready to accept orders<br>**inactive:** Not accepting orders<br>**expired:** Product has time slots, but none of them are open.<br>**sold_out:** Either product or all open time slots are fully booked
token | false | The token uniquely identifying a product on Occasion, in place of ID. **Cannot be used in place of ID in calls, yet, unless as** `GET /products?token=[token]`
post_transactional_message | true | The message to display after an order has been completed
price | true | The base price of the order, before applying price changing questions, tax, coupons, gift cards, etc.
time_slots_closed_before | true | The point in time before which time slots are closed for sales. Any time slot occurring between Time.now and the actual occurrence of that time slot (when the class takes place) cannot be sold.
embed_button_text | true | The text to display in an embed button that opens an order widget
show_occurrence_availability | true | If `true`, show how many open seats there are for a time slot
tax_percentage | true | The sales tax percentage that is applied to the subtotal of an order for this product
widget_contact_title | true | The title to display above a section regarding customer contact information (email, first_name, last_name, zip)
widget_occurrences_title | true | The title to display above a section regarding choosing a time slot
widget_attributes_title | true | The title to display above a section asking additional questions based off custom attributes
widget_payment_title | true | The title to display above a section asking for payment information like credit card details
widget_total_due_title | true | The title to display above a section indicating the total price of the order
widget_gift_card_recipient_title | true | The title to display above a section asking for the details of a gift card recipient (name, email, personal message), if the product `sells_gift_cards`
template_id | false | The ID of the template product that this product has been duplicated from
capacity | false | The amount of orders that can be reserved (booked but having not occurred yet) for a product
show_time_slot_duration | true | If `true`, display the duration of a time slot
sells_gift_cards | true | If `true`, display the gift card attributes in an order widget and create a gift card with the order, with a value equal to the total price of the order
gift_card_redemption_message | false | The message to display in additional to a gift card's personal message, typically instructing a recipient on how to redeem their gift card
from_name | false | The `from` name on the email sent to a customer after they complete an order
email_subject | false | The `subject` line on the email sent to a customer after they complete an order
url | true | The short URL to send someone to to purchase an order for a product

### Associations

Possible associations to include are:

Association | Default | Public | Description
----------- | ------- | ------ | -----------
merchant | false | true | The merchant that the product belongs to
venue | false | true | The venue that the product belongs to
