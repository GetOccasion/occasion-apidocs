# Redeemables (Coupons, Gift Cards)

## Check A Possible Redeemable Code For A Product

```shell
curl "https://app.getoccasion.com/api/v1/products/:id/redeemables?filter[code]=COUPON-CODE"
  -u "59a8517fd9458b46d4ee59f8fd717fb80d:de7b7ae9e2e9e01a9508290e599"
```

```http
HTTPS/1.1 200 OK
```

```json
[
  {
    "data": {
      "type": "coupons",
      "id": "h17sle7",
      "attributes": {
        "name": "Holiday Coupon",
        "code": "COUPON-CODE",
        "discount_fixed": 2.0,
        "discount_percentage": null
      }
    }
  }
]
```

```shell
curl "https://app.getoccasion.com/api/v1/products/:id/redeemables?filter[code]=GIFT-CARD-CODE"
  -u "59a8517fd9458b46d4ee59f8fd717fb80d:de7b7ae9e2e9e01a9508290e599"
```

```http
HTTPS/1.1 200 OK
```

```json
[
  {
    "data": {
      "type": "gift_cards",
      "id": "h17sle7",
      "attributes": {
        "code": "GIFT-CARD-CODE",
        "initial_value": 50.0,
        "value": 5.0
      }
    }
  }
]
```

This endpoint requires a `filter[code]` that is either the code for a coupon that is available for the product, or a gift card that may
be able to be used to purchase the product. Use this to check that a code is valid, and retrieve the necessary `id` that is required to create
orders that are purchased using coupons and gift cards.

### HTTP Request

`GET https://app.getoccasion.com/api/v1/products/:id/redeemables?filter[code]=COUPON-OR-GIFT-CARD-CODE`

### URL Parameters

Parameter | Description | Required
--------- | ----------- | ---------
id | The ID of the product to retrieve redeemables for. | true
filter | The filter params to apply to collection of redeemables for the product. | true
&#x203a; code | The code of the coupon or gift card that may possibly be used to purchase this product. | false

### Response Body

Notable response fields for `coupons` include:

Field | Public | Description
----- | ------ | -----------
name | true | The name of the coupon.
code | true | The coupon code.
discount_fixed | true | The fixed cash discount for the coupon. If `null`, then coupon is percentage discount.
discount_percentage | true | The percentage discount for the coupon. If `null`, then coupon is fixed discount.

Notable response fields for `gift_cards` include:

Field | Public | Description
----- | ------ | -----------
code | true | The gift card code.
initial_value | true | The initial value that was loaded onto the gift card.
value | true | The remaining value on the gift card.
