# Products

## Get All Products

```shell
curl "http://app.getoccasion.com/api/v1/products"
  -u "59a8517fd9458b46d4ee59f8fd717fb80d:de7b7ae9e2e9e01a9508290e599"
```

```http
HTTPS/1.1 200 OK
```

```json
{
  "data": [
    {
      "type": "products",
      "id": "38asnd2",
      "attributes": {
        "image": {
          "url": "https://s3.amazonaws.com/development.assets.playoccasion/uploads/product/image/xxxxx/xxxxx.jpg",
          "thumb": {
            "url": "https://s3.amazonaws.com/development.assets.playoccasion/uploads/product/image/xxxxx/xxxxx.jpg"
          }
        },
        "title": "My Art Class",
        "description": "Sign up to paint a teapot.",
        "status": "active",
        "created_at": "2015-10-23T11:00:44.539-05:00",
        "updated_at": "2015-10-23T11:00:44.539-05:00",
        "price": "10.0",
        "tax_percentage": "3.75",
        "closing_time_relative": true,
        "time_slots_closed_before": "2000-01-01T00:00:00.000Z",
        "show_occurrence_availability": true,
        "show_time_slot_duration": false,
        "widget_contact_title": "Customer Information",
        "widget_occurrences_title": "Select which day you would like to reserve",
        "widget_attributes_title": "Additional Questions",
        "widget_payment_title": "Payment Information",
        "widget_total_due_title": "Total Due Today",
        "order_button_text": "Finalize order",
        "post_transactional_message": "Thank you for ordering."
      }
    }
  ]
}
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
status | true | The status that will determine if the product is active for ordering.<br><br>*Possible values:*<br>**active:** Ready to accept orders<br>**inactive:** Not accepting orders<br>**expired:** Product has time slots, but none of them are open.<br>**sold_out:** Either product or all open time slots are fully booked
price | true | The base price of the order, before applying price changing questions, tax, coupons, gift cards, etc.
tax_percentage | true | The sales tax percentage that is applied to an order for this product
closing_time_relative | true | Whether or not `time_slots_closed_before` below indicates time relative to the time_slot start datetime, or absolute to the current day
time_slots_closed_before | true | The point in time before which time slots are closed for sales. Any time slot occurring between Time.now and the actual occurrence of that time slot (when the class takes place) cannot be sold.
show_occurrence_availability | true | If `true`, show how many open seats there are for a time slot
show_time_slot_duration | true | If `true`, display the duration of a time slot
widget_contact_title | true | The title to display above a section regarding customer contact information (email, first_name, last_name, zip)
widget_occurrences_title | true | The title to display above a section regarding choosing a time slot
widget_attributes_title | true | The title to display above a section asking additional questions based off custom attributes
widget_payment_title | true | The title to display above a section asking for payment information like credit card details
widget_total_due_title | true | The title to display above a section indicating the total price of the order
order_button_text | true | The text to display in the submit order button on an order widget
post_transactional_message | true | The message to display after an order has been completed

### Associations

Possible associations to include are:

Association | Description
----------- | -----------
attrs | The attributes of the product (questions to answer for an order)
merchant | The merchant that the product belongs to
venue | The venue that the product belongs to

## Get a Specific Product

```shell
curl "http://app.getoccasion.com/api/v1/products/38asnd2"
  -u "59a8517fd9458b46d4ee59f8fd717fb80d:de7b7ae9e2e9e01a9508290e599"
```

```http
HTTPS/1.1 200 OK
```

```json
{
  "data": {
    "type": "products",
    "id": "38asnd2",
    "attributes": {
      "image": {
        "url": "https://s3.amazonaws.com/development.assets.playoccasion/uploads/product/image/xxxxx/xxxxx.jpg",
        "thumb": {
          "url": "https://s3.amazonaws.com/development.assets.playoccasion/uploads/product/image/xxxxx/xxxxx.jpg"
        }
      },
      "title": "My Art Class",
      "description": "Sign up to paint a teapot.",
      "status": "active",
      "created_at": "2015-10-23T11:00:44.539-05:00",
      "updated_at": "2015-10-23T11:00:44.539-05:00",
      "price": "10.0",
      "tax_percentage": "3.75",
      "closing_time_relative": true,
      "time_slots_closed_before": "2000-01-01T00:00:00.000Z",
      "show_occurrence_availability": true,
      "show_time_slot_duration": false,
      "widget_contact_title": "Customer Information",
      "widget_occurrences_title": "Select which day you would like to reserve",
      "widget_attributes_title": "Additional Questions",
      "widget_payment_title": "Payment Information",
      "widget_total_due_title": "Total Due Today",
      "order_button_text": "Finalize order",
      "post_transactional_message": "Thank you for ordering."
    }
  }
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

Notable response fields include:

Field | Public | Description
----- | ------ | -----------
image | true | URLs for the full image and thumbnail to display with a product
title | true | The title of the product, such as "BYOB & Paint A Forest"
description | true | The description for the product, explaining things in detail
status | true | The status that will determine if the product is active for ordering.<br><br>*Possible values:*<br>**active:** Ready to accept orders<br>**inactive:** Not accepting orders<br>**expired:** Product has time slots, but none of them are open.<br>**sold_out:** Either product or all open time slots are fully booked
price | true | The base price of the order, before applying price changing questions, tax, coupons, gift cards, etc.
tax_percentage | true | The sales tax percentage that is applied to an order for this product
closing_time_relative | true | Whether or not `time_slots_closed_before` below indicates time relative to the time_slot start datetime, or absolute to the current day
time_slots_closed_before | true | The point in time before which time slots are closed for sales. Any time slot occurring between Time.now and the actual occurrence of that time slot (when the class takes place) cannot be sold.
show_occurrence_availability | true | If `true`, show how many open seats there are for a time slot
show_time_slot_duration | true | If `true`, display the duration of a time slot
widget_contact_title | true | The title to display above a section regarding customer contact information (email, first_name, last_name, zip)
widget_occurrences_title | true | The title to display above a section regarding choosing a time slot
widget_attributes_title | true | The title to display above a section asking additional questions based off custom attributes
widget_payment_title | true | The title to display above a section asking for payment information like credit card details
widget_total_due_title | true | The title to display above a section indicating the total price of the order
order_button_text | true | The text to display in the submit order button on an order widget
post_transactional_message | true | The message to display after an order has been completed

### Associations

Possible associations to include are:

Association | Description
----------- | -----------
attrs | The attributes of the product (questions to answer for an order)
merchant | The merchant that the product belongs to
venue | The venue that the product belongs to

## Get a Specific Product So You Can Order It

```shell
curl "http://app.getoccasion.com/api/v1/products?include=attrs.attribute_options,attrs.field_type"
  -u "59a8517fd9458b46d4ee59f8fd717fb80d:de7b7ae9e2e9e01a9508290e599"
```

```http
HTTPS/1.1 200 OK
```

```json
{
  "data": {
    "type": "products",
    "id": "38asnd2",
    "attributes": {
      "image": {
        "url": "https://s3.amazonaws.com/development.assets.playoccasion/uploads/product/image/xxxxx/xxxxx.jpg",
        "thumb": {
          "url": "https://s3.amazonaws.com/development.assets.playoccasion/uploads/product/image/xxxxx/xxxxx.jpg"
        }
      },
      "title": "My Art Class",
      "description": "Sign up to paint a teapot.",
      "status": "active",
      "created_at": "2015-10-23T11:00:44.539-05:00",
      "updated_at": "2015-10-23T11:00:44.539-05:00",
      "price": "10.0",
      "tax_percentage": "3.75",
      "closing_time_relative": true,
      "time_slots_closed_before": "2000-01-01T00:00:00.000Z",
      "show_occurrence_availability": true,
      "show_time_slot_duration": false,
      "widget_contact_title": "Customer Information",
      "widget_occurrences_title": "Select which day you would like to reserve",
      "widget_attributes_title": "Additional Questions",
      "widget_payment_title": "Payment Information",
      "widget_total_due_title": "Total Due Today",
      "order_button_text": "Finalize order",
      "post_transactional_message": "Thank you for ordering."
    },
    "relationships": {
      "attrs": {
        "data": [
          { "type": "attributes", "id": "h6sbeekj" },
          { "type": "attributes", "id": "72yas0iu" }
        ]
      }
    }
  },
  "included": [
    {
      "type": "attributes",
      "id": "h6sbeekj",
      "attributes": {
        "title": "Which option to this question do you prefer?",
        "created_at": "2015-10-23T11:00:44.539-05:00",
        "updated_at": "2015-10-23T11:00:44.539-05:00",
        "position": 0,
        "parameters": {
        }
      },
      "relationships": {
        "attribute_options": {
          "data": [
            { "type": "attribute_options", "id": "j36ehac" },
            { "type": "attribute_options", "id": "8asbdye" }
          ]
        },
        "field_type": {
          "data": {
            "type": "field_types",
            "id": "17hejas"
          }
        }
      }
    },
    {
      "type": "attributes",
      "id": "72yas0iu",
      "attributes": {
        "title": "What input do you have?",
        "created_at": "2015-10-23T11:00:44.539-05:00",
        "updated_at": "2015-10-23T11:00:44.539-05:00",
        "position": 0,
        "parameters": {
        }
      },
      "relationships": {
        "field_type": {
          "data": {
            "type": "field_types",
            "id": "mn2l6eh"
          }
        }
      }
    },
    {
      "type": "attribute_options",
      "id": "j36ehac",
      "attributes": {
        "title": "Option 1 ($50)",
        "created_at": "2015-10-23T11:00:44.539-05:00",
        "updated_at": "2015-10-23T11:00:44.539-05:00",
        "position": 0,
        "default": true,
        "parameters": {
          "price": 50.0
        }
      }
    },
    {
      "type": "attribute_options",
      "id": "8asbdye",
      "attributes": {
        "title": "Option 2 ($100)",
        "created_at": "2015-10-23T11:00:44.539-05:00",
        "updated_at": "2015-10-23T11:00:44.539-05:00",
        "position": 1,
        "default": false,
        "parameters": {
          "price": 100.0
        }
      }
    },
    {
      "type": "field_types",
      "id": "17hejas",
      "attributes": {
        "created_at": "2015-10-23T11:00:44.539-05:00",
        "updated_at": "2015-10-23T11:00:44.539-05:00",
        "category": "price",
        "form_control": "drop_down",
        "operation": "adding",
        "reflective": false
      }
    },
    {
      "type": "field_types",
      "id": "mn2l6eh",
      "attributes": {
        "created_at": "2015-10-23T11:00:44.539-05:00",
        "updated_at": "2015-10-23T11:00:44.539-05:00",
        "category": "info",
        "form_control": "text_input",
        "operation": null,
        "reflective": false
      }
    }
  ]
}
```

This request retrieves a specific product with its attributes, which are needed to order the product.

### HTTP Request

`GET http://example.com/api/v1/products/:id?include=attrs.attribute_options,attrs.field_types`

### URL Parameters

Parameter | Description
--------- | -----------
id | The ID of the product to retrieve

### Response Body

Notable response fields include:

Field | Public | Description
----- | ------ | -----------
image | true | URLs for the full image and thumbnail to display with a product
title | true | The title of the product, such as "BYOB & Paint A Forest"
description | true | The description for the product, explaining things in detail
status | true | The status that will determine if the product is active for ordering.<br><br>*Possible values:*<br>**active:** Ready to accept orders<br>**inactive:** Not accepting orders<br>**expired:** Product has time slots, but none of them are open.<br>**sold_out:** Either product or all open time slots are fully booked
price | true | The base price of the order, before applying price changing questions, tax, coupons, gift cards, etc.
tax_percentage | true | The sales tax percentage that is applied to an order for this product
closing_time_relative | true | Whether or not `time_slots_closed_before` below indicates time relative to the time_slot start datetime, or absolute to the current day
time_slots_closed_before | true | The point in time before which time slots are closed for sales. Any time slot occurring between Time.now and the actual occurrence of that time slot (when the class takes place) cannot be sold.
show_occurrence_availability | true | If `true`, show how many open seats there are for a time slot
show_time_slot_duration | true | If `true`, display the duration of a time slot
widget_contact_title | true | The title to display above a section regarding customer contact information (email, first_name, last_name, zip)
widget_occurrences_title | true | The title to display above a section regarding choosing a time slot
widget_attributes_title | true | The title to display above a section asking additional questions based off custom attributes
widget_payment_title | true | The title to display above a section asking for payment information like credit card details
widget_total_due_title | true | The title to display above a section indicating the total price of the order
order_button_text | true | The text to display in the submit order button on an order widget
post_transactional_message | true | The message to display after an order has been completed
attrs | true | The attributes of the product. Each has a value in an order for this product.
&#x203a; title | true | The title of the attribute - the question to be answered.
&#x203a; position | true | The position of this question in the order form
&#x203a; parameters | true | Object containing optional parameters for the attribute
&#x203a; attribute_options | true | Options for the attribute, if it is a drop down or other option based form control
&#x203a;&#x203a; title | true | The title of the attribute option
&#x203a;&#x203a; position | true | The position of the attribute option amongst its siblings
&#x203a;&#x203a; default | true | Whether or not this attribute option should be selected by default
&#x203a;&#x203a; parameters | true | Object containing optional parameters for the attribute option
&#x203a;&#x203a;&#x203a; price | true | The price of the attribute option
&#x203a; field_type | true | The field type / form control of the attribute
&#x203a;&#x203a; category | true | What type of attribute is this: `'info'`, `'price'`, `'permutable'`, `'discount'`, `'static'`
&#x203a;&#x203a; form_control | true| The form_control type for the attribute: `'text_input'`,`'drop_down'`,`'checkbox'`,`'option_list'`,`'spin_button'`,`'text_area'`,`'separator'`,`'text_output'`
&#x203a;&#x203a; operation | true | The type of mathematical operation the attribute does to the price of the order: `'adding'`,`'multiplying'`,`'subtracting'`,`'dividing'`
&#x203a;&#x203a; reflective | true | Whether or not this field type is one that will reflect on the value of another attribute in the product when choosing how to affect the order price.

### Associations

Possible associations to include are:

Association | Description
----------- | -----------
attrs | The attributes of the product (questions to answer for an order)
attrs.attribute_options | The options of each attribute of the product
attrs.field_type | The field type for each attribute of the product
merchant | The merchant that the product belongs to
venue | The venue that the product belongs to