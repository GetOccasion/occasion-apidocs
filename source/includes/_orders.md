# Orders

## Get All Orders

```shell
curl "https://app.getoccasion.com/api/v1/orders"
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
        "created_at": "2015-10-23T11:00:44.539-05:00",
        "updated_at": "2015-10-23T11:00:44.539-05:00",
        "price": "15.0",
        "tax": "0.0",
        "tax_percentage": "10.0",
        "coupon_amount": "1.0",
        "coupon_description": "$1.00",
        "quantity": 1,
        "description": "This is the title of the product ordered.",
        "balance": "0.0",
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
description | true | The title of the product or order items purchased with this order
balance | false | The total balance of accepted transactions paid to this order
session_identifier | false | A unique identifier used to associate this order with a session of an order form (conversion tracking, etc.)
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
gift_card | The gift card that may have been purchased by this order
merchant | The merchant that sold this order
occurrences | Occurrences of the timeslots that were purchased by the order
order_items | The items purchased with the order, instead of a product
product | The product that the order is for
transactions | Transactions to pay for the order

## Get a Specific Order

```shell
curl "https://app.getoccasion.com/api/v1/orders/38asnd2"
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
      "created_at": "2015-10-23T11:00:44.539-05:00",
      "updated_at": "2015-10-23T11:00:44.539-05:00",
      "price": "15.4",
      "tax": "1.40",
      "tax_percentage": "10.0",
      "coupon_amount": "1.0",
      "coupon_description": "$1.00",
      "quantity": 1,
      "description": "This is the title of the product ordered.",
      "balance": "0.0",
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
description | true | The title of the product or order items purchased with this order
balance | false | The total balance of accepted transactions paid to this order
session_identifier | false | A unique identifier used to associate this order with a session of an order form (conversion tracking, etc.)
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
gift_card | The gift card that may have been purchased by this order
merchant | The merchant that sold this order
occurrences | Occurrences of the timeslots that were purchased by the order
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
      "session_identifier": "any-unique-key",
    },
    "relationships": {
      "attribute_values": {
        "data": [
          {
            "type": "attribute_values",
            "attributes": {
              "value": "6shen2as"
            },
            "relationships": {
              "attribute": {
                "data": { "type": "attributes", "id": "12n83qa" }
              }
            }
          },
          {
            "type": "attribute_values",
            "attributes": {
              "value": "Text value"
            },
            "relationships": {
              "attribute": {
                "data": { "type": "attributes", "id": "82has32" }
              }
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
      "time_slots": {
        "data": [
          { "type": "time_slots", "id": "7hwq5de" },
          { "type": "time_slots", "id": "97eh2sa" }
        ]
      },
      "transactions": {
        "data": [
          {
            "type": "transactions",
            "attributes": {
              "amount": "5.0",
            },
            "relationships": {
              "payment_method": {
                "data": { "type": "credit_cards", "id": "H7gJ8GtEfCdLi88uRD6FhfrtOPTizjt" }
              }
            }
          },
          {
            "type": "transactions",
            "attributes": {
              "amount": "5.0",
            },
            "relationships": {
              "payment_method": {
                "data": { "type": "gift_cards", "id": "D3HJ8GtEfCdLixGh3D6FhfrtOPTh6w5e" }
              }
            }
          },
          {
            "type": "transactions",
            "attributes": {
              "amount": "5.0",
            },
            "relationships": {
              "payment_method": {
                "data": { "type": "paypals", "id": "3D6FhfrtOPTh6w5eH7gJ8GtEfCdL" }
              }
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
      "created_at": "2015-10-23T11:00:44.539-05:00",
      "updated_at": "2015-10-23T11:00:44.539-05:00",
      "price": "10.0",
      "tax": "0.0",
      "tax_percentage": "10.0",
      "coupon_amount": "1.0",
      "coupon_description": "$1.00",
      "quantity": 1,
      "description": "This is the title of the product ordered.",
      "balance": "0.0",
      "session_identifier": "any-unique-key",
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
attribute_values | Values for each attribute of the product being ordered | false
&#x203a;attribute | The attribute this attribute_value is for | true
&#x203a;value | The value or "answer" for the attribute. If the attribute has attribute_options, this value will be the ID of the selected attribute option. Otherwise, it is just a value. | true
coupon | The coupon used to receive a discount on the order | false
customer | The customer purchasing the order | true
&#x203a;email | The email of the customer | true
&#x203a;first_name | The first name of the customer | true
&#x203a;last_name | The last name of the customer | true
&#x203a;zip | The zip of the customer | true
product | The product being ordered | true
time_slots | The time slots being ordered | true
transactions | The transactions (credit card, paypal, gift card) that pay for the order. The total amount paid for across transactions must equal the order price. | If order has price
&#x203a;amount | The amount that this transaction is paying for. | true
&#x203a;payment_method | The payment method used to purchase the transaction.<br><br>*Possible types:*<br>**credit_cards**<br>**gift_cards**<br>**paypals** | true

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
description | true | The title of the product or order items purchased with this order
balance | false | The total balance of accepted transactions paid to this order
session_identifier | false | A unique identifier used to associate this order with a session of an order form (conversion tracking, etc.)
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
gift_card | The gift card that may have been purchased by this order
merchant | The merchant that sold this order
occurrences | Occurrences of the timeslot that the order was purchased for
order_items | The items purchased with the order, instead of a product
product | The product that the order is for
transactions | Transactions to pay for the order

## Get The Price Of An Order

```http
POST /api/v1/orders/price HTTPS/1.1
Host: app.getoccasion.com
Authorization: Basic NTlhZTdiN2FlOWUyZTllMDFhOTUwODI5MGU1OTk=
Content-Type: application/json
```

```json
{
  "data": {
    "type": "orders",
    "relationships": {
      "attribute_values": {
        "data": [
          {
            "type": "attribute_values",
            "attributes": {
              "value": "6shen2as"
            },
            "relationships": {
              "attribute": {
                "data": { "type": "attributes", "id": "12n83qa" }
              }
            }
          }
        ]
      },
      "coupon": {
        "data": { "type": "coupons", "id": "gYw6eas" }
      },
      "product": {
        "data": { "type": "products", "id": "bteyn26" }
      }
    }
  }
}
```

```http
HTTPS/1.1 200 OK
```

```json
{
  "data": {
    "type": "orders",
    "attributes": {
      "subtotal": "10.0",
      "coupon_amount": "1.0",
      "tax": "2.0",
      "total": "11.0"
    }
  }
}
```

This endpoint calculates the price of an order

### HTTP Request

`POST https://app.getoccasion.com/api/v1/orders/price`

### Request Body

Field | Description | Required?
----- | ----------- | ---------
attribute_values | Values for the attributes that affect the price of the order | false
&#x203a;attribute | The attribute this attribute_value is for | true
&#x203a;value | The value or "answer" for the attribute. If the attribute has attribute_options, this value will be the ID of the selected attribute option. Otherwise, it is just a value. | true
coupon | The coupon that has an impact on the price of the order | false
product | The product that defines the base price, attributes, and tax_percentage of the order | true

### Response Body

Notable response fields include:

Field | Description
----- | -----------
subtotal | The price of the order before adding tax or coupons. product.price + attributes
coupon_amount | The amount that the coupon discounts from the order
tax | The amount paid in tax, based on the tax_percentage
total | The final price of the order that is to be paid by the customer
