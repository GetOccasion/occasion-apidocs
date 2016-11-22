# Orders

## Get All Orders

```shell
curl "http://app.getoccasion.com/api/v1/orders"
  -u "59a8517fd9458b46d4ee59f8fd717fb80d:de7b7ae9e2e9e01a9508290e599"
```

```http
HTTPS/1.1 200 OK
```

```json
{
  "data": [
    {
      "type": "orders",
      "id": "38asnd2",
      "attributes": {
        "verification_code": "kASn37a",
        "status": "booked",
        "price": 15.0,
        "tax": 0.0,
        "tax_percentage": 10.0,
        "coupon_amount": 1.0,
        "coupon_description": "$1.00",
        "quantity": 1,
        "summary": "This is a complex summary of the order.",
        "description": "This is the title of the product ordered.",
        "balance": 0.0,
        "session_identifier": "k37a8h-uw7gnc5-jqy6D0-k9287a",
        "customer_name": "Jane Smith",
        "customer_email": "jane@example.com",
        "customer_zip": "00000",
        "payment_status": "completed"
      }
    }
  ]
}
```

This endpoint retrieves all orders.

### HTTP Request

`GET https://app.getoccasion.com/api/v1/orders`

### Response Body

Notable response fields include:

Field | Public | Description
----- | ------ | -----------
verification_code | true | A reference code assigned to the order after it has been completed
status | true | The status of the order<br><br>*Possible values:*<br>**booked:** Order was successfully completed and paid for.<br>**reserved:** Order was completed, and payment will be made at a later time.<br>**dropped:** The order was not successfully completed, because a payment failed.<br>**canceled:** The order was canceled and then refunded.
price | true | The total price of the order after tax, coupons, etc.
tax | true | The total sales tax for the order
tax_percentage | true | The sales tax percentage that was applied to the order
coupon_amount | true | The amount that the coupon used for this order took off from the order price
coupon_description | true | A readable version of the coupon amount: if a fixed discount coupon, then `'$X.XX'`, if a percentage discount, then `'X.X%'`
quantity | true | The quantity of this order that was purchased
summary | true | A lengthy description of the order, incorporating multiple elements to "summarize" the completed order to the customer
description | true | The title of the product or order items purchased with this order
balance | false | The total balance left to be paid on this order
session_identifier | false | An identifier used to associate this order with a session of an order form (conversion tracking, etc.)
customer_name | false | The name the customer used to purchase this order
customer_email | false | The email the customer used to purchase this order
customer_zip | false | The zip code the customer used to purchase this order
payment_status | false | The status of the payments for this order<br><br>*Possible values:*<br>**completed:** Order payments were successfully completed.<br>**awaiting_customer_payment:** Customer was redirected to complete payment and we're awaiting this completion.<br>**processing:** Payments have been made, but are still processing through providers.<br>**failed:** Payment(s) failed for some reason.

### Associations

Possible associations to include are:

Association | Description
----------- | -----------
attribute_values | The values for attributes of the product the order is for
comments | Comments made on the order by the merchant
coupon | The coupon used with the order
currency | The currency used to purchase the order
customer | The customer that purchased the order
merchant | The merchant that sold this order
occurrences | Occurrences of the timeslot that the order was purchased for
product | The product that the order is for
transactions | Transactions to pay for the order

## Get a Specific Order

```shell
curl "http://app.getoccasion.com/api/v1/orders/38asnd2"
  -u "59a8517fd9458b46d4ee59f8fd717fb80d:de7b7ae9e2e9e01a9508290e599"
```

```http
HTTPS/1.1 200 OK
```

```json
{
  "data": {
    "type": "orders",
    "id": "38asnd2",
    "attributes": {
      "verification_code": "kASn37a",
      "status": "booked",
      "price": 15.4,
      "tax": 1.40,
      "tax_percentage": 10.0,
      "coupon_amount": 1.0,
      "coupon_description": "$1.00",
      "quantity": 1,
      "summary": "This is a complex summary of the order.",
      "description": "This is the title of the product ordered.",
      "balance": 0.0,
      "session_identifier": "k37a8h-uw7gnc5-jqy6D0-k9287a",
      "customer_name": "Jane Smith",
      "customer_email": "jane@example.com",
      "customer_zip": "00000",
      "payment_status": "completed"
    }
  }
}
```

This endpoint retrieves a specific order.

### HTTP Request

`GET https://app.getoccasion.com/api/v1/orders/:id`

### URL Parameters

Parameter | Description
--------- | -----------
id | The ID of the order to retrieve

### Response Body

Notable response fields include:

Field | Public | Description
----- | ------ | -----------
verification_code | true | A reference code assigned to the order after it has been completed
status | true | The status of the order<br><br>*Possible values:*<br>**booked:** Order was successfully completed and paid for.<br>**reserved:** Order was completed, and payment will be made at a later time.<br>**dropped:** The order was not successfully completed, because a payment failed.<br>**canceled:** The order was canceled and then refunded.
price | true | The total price of the order after tax, coupons, etc.
tax | true | The total sales tax for the order
tax_percentage | true | The sales tax percentage that was applied to the order
coupon_amount | true | The amount that the coupon used for this order took off from the order price
coupon_description | true | A readable version of the coupon amount: if a fixed discount coupon, then `'$X.XX'`, if a percentage discount, then `'X.X%'`
quantity | true | The quantity of this order that was purchased
summary | true | A lengthy description of the order, incorporating multiple elements to "summarize" the completed order to the customer
description | true | The title of the product or order items purchased with this order
balance | false | The total balance left to be paid on this order
session_identifier | false | An identifier used to associate this order with a session of an order form (conversion tracking, etc.)
customer_name | false | The name the customer used to purchase this order
customer_email | false | The email the customer used to purchase this order
customer_zip | false | The zip code the customer used to purchase this order
payment_status | false | The status of the payments for this order<br><br>*Possible values:*<br>**completed:** Order payments were successfully completed.<br>**awaiting_customer_payment:** Customer was redirected to complete payment and we're awaiting this completion.<br>**processing:** Payments have been made, but are still processing through providers.<br>**failed:** Payment(s) failed for some reason.

### Associations

Possible associations to include are:

Association | Description
----------- | -----------
attribute_values | Values for attributes of the product the order is for
comments | Comments made on the order by the merchant
coupon | The coupon used with the order
currency | The currency used to purchase the order
customer | The customer that purchased the order
merchant | The merchant that sold this order
occurrences | Occurrences of the timeslot that the order was purchased for
order_items | The items purchased with the order, instead of a product
product | The product that the order is for
transactions | Transactions to pay for the order

## Create an Order

```http
POST /api/v1/orders HTTPS/1.1
Host: app.getoccasion.com
Authorization: Basic NTlhZTdiN2FlOWUyZTllMDFhOTUwODI5MGU1OTk=
Content-Type: application/json
```

```json
{
  "data": {
    "type": "orders",
    "attributes": {
      "session_identifier": "any-key-you-want",
      "time_slot_id": "2016090823451"
    },
    "relationships": {
      "attribute_values": {
        "data": [
          {
            "type": "attribute_values",
            "attributes": {
              "attr_id": "12n83qa",
              "value": "6shen2as"
            }
          },
          {
            "type": "attribute_values",
            "attributes": {
              "attr_id": "82has32",
              "value": "Text value"
            }
          }
        ]
      },
      "coupon": {
        "data": { "type": "coupons", "id": "gYw6eas" }
      },
      "customer": {
        "data": {
          "type": "customers",
          "attributes": {
            "email": "jane@example.com",
            "first_name": "Jane",
            "last_name": "Smith",
            "zip": "60000"
          }
        }
      },
      "product": {
        "data": { "type": "products", "id": "bteyn26" }
      },
      "transactions": {
        "data": [
          {
            "type": "transactions",
            "attributes": {
              "amount": 5.0,
              "payment_method_token": "H7gJ8GtEfCdLi88uRD6FhfrtOPTizjt"
            }
          },
          {
            "type": "transactions",
            "attributes": {
              "amount": 5.0,
              "gift_card_code": "CODE1X"
            }
          }
        ]
      }
    }
  }
}
```

```http
HTTPS/1.1 201 Created
```

```json
{
  "data": {
    "type": "orders",
    "id": "38asnd2",
    "attributes": {
      "verification_code": "kASn37a",
      "status": "booked",
      "price": 10.0,
      "tax": 0.0,
      "tax_percentage": 10.0,
      "coupon_amount": 1.0,
      "coupon_description": "$1.00",
      "quantity": 1,
      "summary": "This is a complex summary of the order.",
      "description": "This is the title of the product ordered.",
      "balance": 0.0,
      "session_identifier": "any-key-you-want",
      "customer_name": "Jane Smith",
      "customer_email": "jane@example.com",
      "customer_zip": "00000",
      "payment_status": "completed"
    }
  }
}
```

This endpoint creates a new order

### HTTP Request

`POST https://app.getoccasion.com/api/v1/orders`

### Request Body

Field | Description | Required?
----- | ----------- | ---------
session_identifier | An ID you can input for tracking sessions, form data, conversions, etc. | false
time_slot_id | The ID of the time_slot being booked | false
attribute_values | Values for each attribute of the product being ordered | false
&#x203a;attr_id | The id of the attribute this attribute_value is for | true
&#x203a;value | The value or "answer" for the attribute. If the attribute has attribute_options, this value will be the ID of the selected attribute option. Otherwise, it is just a value. | true
coupon | The coupon used to receive a discount on the order | false
customer | The customer purchasing the order | true
&#x203a;email | The email of the customer | true
&#x203a;first_name | The first name of the customer | true
&#x203a;last_name | The last name of the customer | true
&#x203a;zip | The zip of the customer | true
product | The product being ordered | true
transactions | The transactions (credit card, gift card) that pay for the order. The total amount paid for across transactions must equal the order price. | If order has price
&#x203a;amount | The amount that this transaction is paying for. | true
&#x203a;gift_card_code | The code of the gift card being used to pay for this transaction. | false
&#x203a;payment_method_token | The payment method token (from Spreedly), representing a payment method to pay for this transaction | false

### Response Body

Notable response fields include:

Field | Public | Description
----- | ------ | -----------
verification_code | true | A reference code assigned to the order after it has been completed
status | true | The status of the order<br><br>*Possible values:*<br>**booked:** Order was successfully completed and paid for.<br>**reserved:** Order was completed, and payment will be made at a later time.<br>**dropped:** The order was not successfully completed, because a payment failed.<br>**canceled:** The order was canceled and then refunded.
price | true | The total price of the order after tax, coupons, etc.
tax | true | The total sales tax for the order
tax_percentage | true | The sales tax percentage that was applied to the order
coupon_amount | true | The amount that the coupon used for this order took off from the order price
coupon_description | true | A readable version of the coupon amount: if a fixed discount coupon, then `'$X.XX'`, if a percentage discount, then `'X.X%'`
quantity | true | The quantity of this order that was purchased
summary | true | A lengthy description of the order, incorporating multiple elements to "summarize" the completed order to the customer
description | true | The title of the product or order items purchased with this order
balance | false | The total balance left to be paid on this order
session_identifier | false | An identifier used to associate this order with a session of an order form (conversion tracking, etc.)
customer_name | false | The name the customer used to purchase this order
customer_email | false | The email the customer used to purchase this order
customer_zip | false | The zip code the customer used to purchase this order
payment_status | false | The status of the payments for this order<br><br>*Possible values:*<br>**completed:** Order payments were successfully completed.<br>**awaiting_customer_payment:** Customer was redirected to complete payment and we're awaiting this completion.<br>**processing:** Payments have been made, but are still processing through providers.<br>**failed:** Payment(s) failed for some reason.

### Associations

Possible associations to include are:

Association | Description
----------- | -----------
attribute_values | Values for attributes of the product the order is for
comments | Comments made on the order by the merchant
coupon | The coupon used with the order
currency | The currency used to purchase the order
customer | The customer that purchased the order
merchant | The merchant that sold this order
occurrences | Occurrences of the timeslot that the order was purchased for
order_items | The items purchased with the order, instead of a product
product | The product that the order is for
transactions | Transactions to pay for the order
