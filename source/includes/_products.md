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
    "gift_card_redemption_message": "I bought a gift card for you!",
    "from_name": "My name",
    "email_subject": "Someone bought you a gift card!",
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
    "gift_card_redemption_message": "I bought a gift card for you!",
    "from_name": "My name",
    "email_subject": "Someone bought you a gift card!",
    "url": "http://occ.sn/p/n/sdj291"
  }
]
```

This endpoint retrieves all products.

### HTTP Request

`GET http://example.com/api/v1/products`

### Response Body

Notable response fields include:

Field | Description
--------- | -----------
status | The status that will determine if the product is active for ordering.<br><br>*Possible values:*<br>**active:** Ready to accept orders<br>**inactive:** Not accepting orders<br>**expired:** Product has time slots, but none of them are open.<br>**sold_out:** Either product or all open time slots are fully booked.
token | The token uniquely identifying a product on Occasion, in place of ID. **Cannot be used in place of ID in calls, yet, unless as** `GET /products?token=[token]`
time_slots_closed_before | The point in time before which time slots are closed for sales. Any time slot occurring between Time.now and the actual occurrence of that time slot (when the class takes place) cannot be sold.
capacity | The amount of orders that can be reserved (booked but having not occurred yet) for a product.
url | The short URL to send someone to to purchase an order for a product.

### Associations

Possible associations to include are:

Association | Description
----------- | -----------
merchant | The merchant that the product belongs to
venue | The venue that the product belongs to

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
 "gift_card_redemption_message": "I bought a gift card for you!",
 "from_name": "My name",
 "email_subject": "Someone bought you a gift card!",
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
 "gift_card_redemption_message": "I bought a gift card for you!",
 "from_name": "My name",
 "email_subject": "Someone bought you a gift card!",
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

Field | Description
--------- | -----------
status | The status that will determine if the product is active for ordering.<br><br>*Possible values:*<br>**active:** Ready to accept orders<br>**inactive:** Not accepting orders<br>**expired:** Product has time slots, but none of them are open.<br>**sold_out:** Either product or all open time slots are fully booked.
token | The token uniquely identifying a product on Occasion, in place of ID. **Cannot be used in place of ID in calls, yet, unless as** `GET /products?token=[token]`
time_slots_closed_before | The point in time before which time slots are closed for sales. Any time slot occurring between Time.now and the actual occurrence of that timeslot (when the class takes place) cannot be sold.
capacity | The amount of orders that can be reserved (booked but having not occurred yet) for a product.
url | The short URL to send someone to to purchase an order for a product.

### Associations

Possible associations to include are:

Association | Description
----------- | -----------
merchant | The merchant that the product belongs to
venue | The venue that the product belongs to
