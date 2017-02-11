# Merchants

```shell
curl "http://app.getoccasion.com/api/v1/merchants"
  -u "59a8517fd9458b46d4ee59f8fd717fb80d:de7b7ae9e2e9e01a9508290e599"
```

```http
HTTPS/1.1 200 OK
```

```json
{
  "data": [
    {
      "type": "merchants",
      "id": "67sdeas",
      "attributes": {
        "profile_picture": "https://app.getoccasion.com/assets/logo.jpg",
        "created_at": "2015-10-23T11:00:44.539-05:00",
        "updated_at": "2015-10-23T11:00:44.539-05:00",
        "name": "My Business Name",
        "time_zone": "America/Chicago",
        "tax_percentage": "2.0",
        "facebook_page": "https://www.facebook.com/xxxx?fref=ts"
      }
    }
  ]
}
```

This endpoint retrieves the merchant corresponding to your provided API credentials. If you are an Occasion API partner, this endpoint retrieves all merchants under Occasion.

### HTTP Request

`GET https://app.getoccasion.com/api/v1/merchants`

### Response Body

Notable response fields include:

Field | Public | Description
----- | ------ | -----------
profile_picture | true | The URL for the merchant's logo image
name | true | The name of the business
time_zone | true | The timezone that the merchant operates in
tax_percentage | true | The sales tax percentage that the merchant applies to each order subtotal
facebook_page | true | The Facebook page URL for the merchant's business

```shell
curl "http://app.getoccasion.com/api/v1/merchants?include=business_type,currency"
  -u "59a8517fd9458b46d4ee59f8fd717fb80d:de7b7ae9e2e9e01a9508290e599"
```

```http
HTTPS/1.1 200 OK
```

```json
{
  "data": [
    {
      "type": "merchants",
      "id": "67sdeas",
      "attributes": {
        "profile_picture": "https://app.getoccasion.com/assets/logo.jpg",
        "created_at": "2015-10-23T11:00:44.539-05:00",
        "updated_at": "2015-10-23T11:00:44.539-05:00",
        "name": "My Business Name",
        "time_zone": "America/Chicago",
        "tax_percentage": "2.0",
        "facebook_page": "https://www.facebook.com/xxxx?fref=ts"
      },
      "relationships": {
        "business_type": {
          "data": {
            "type": "business_types",
            "id": "k87a7w"
          }
        },
        "currency": {
          "data": {
            "type": "currencies",
            "id": "7ek2ya"
          }
        }
      }
    }
  ],
  "included": [
    {
      "type": "business_types",
      "id": "k87a7w",
      "attributes": {
        "name": "Ice Rink",
      }
    },
    {
      "type": "currencies",
      "id": "7ek2ya",
      "attributes": {
        "name": "USD",
        "code": "$"
      }
    }
  ]
}
```

### Associations

Possible associations to include are:

Association | Description
----------- | -----------
business_type | The type of business that the merchant is
currency | The currency that the merchant accepts
venues | The venues that the merchant operates
