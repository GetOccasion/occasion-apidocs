# Venues

## Get All Venues

```shell
curl "https://app.getoccasion.com/api/v1/venues"
  -u "59a8517fd9458b46d4ee59f8fd717fb80d:de7b7ae9e2e9e01a9508290e599"
```

```http
HTTPS/1.1 200 OK
```

```json
{
  "data": [
    {
      "type": "venues",
      "id": "n2hs7dh",
      "attributes": {
        "name": "The Playplace",
        "address": "123 Main Street",
        "city": "Chicago",
        "zip": "60614",
        "website": "www.example.com",
        "email": "admin@example.com",
        "capacity": 100,
        "phone": "(999) 999-9999",
        "public": "true",
        "time_zone": "America/Chicago"
      }
    }
  ]
}
```

This endpoint retrieves all venues. If made in a public context, only venues `where(public: true)` are returned.

### HTTP Request

`GET https://app.getoccasion.com/api/v1/venues`

### Response Body

Notable response fields include:

Field | Public | Description
----- | ------ | -----------
name | true | The name of the venue
address | true | The street address of the venue
city | true | The city the venue is located in
zip | true | The ZIP code of the venue
website | true | The venue's website
email | true | The email of the venue
capacity | false | The number of open orders that a venue can have for any product
phone | true | The phone number of the venue
public | false | If `false`, the venue should not be displayed as open for business
time_zone | true | The time zone that the venue operates in

### Associations

Possible associations to include are:

Association | Description
----------- | -----------
country | The country the venue is in
state | The state/province the venue is in
merchant | The merchant that the venue belongs to
products | All the products offered at the venue

## Get a Specific Venue

```shell
curl "https://app.getoccasion.com/api/v1/venues/n2hs7dh"
  -u "59a8517fd9458b46d4ee59f8fd717fb80d:de7b7ae9e2e9e01a9508290e599"
```

```http
HTTPS/1.1 200 OK
```

```json
{
  "data": {
    "type": "venues",
    "id": "n2hs7dh",
    "attributes": {
      "name": "The Playplace",
      "address": "123 Main Street",
      "city": "Chicago",
      "zip": "60614",
      "website": "www.example.com",
      "email": "admin@example.com",
      "capacity": 100,
      "phone": "(999) 999-9999",
      "public": "true",
      "time_zone": "America/Chicago"
    }
  }
}
```

This endpoint retrieves a specific venue. If made in a public context, only a venue `where(public: true)` can be returned.

### HTTP Request

`GET https://app.getoccasion.com/api/v1/venues/:id`

### URL Parameters

Parameter | Description
--------- | -----------
id | The ID of the venue to retrieve

### Response Body

Notable response fields include:

Field | Public | Description
----- | ------ | -----------
name | true | The name of the venue
address | true | The street address of the venue
city | true | The city the venue is located in
zip | true | The ZIP code of the venue
website | true | The venue's website
email | true | The email of the venue
capacity | false | The number of open orders that a venue can have for any product
phone | true | The phone number of the venue
public | false | If `false`, the venue should not be displayed as open for business
time_zone | true | The time zone that the venue operates in

### Associations

Possible associations to include are:

Association | Description
----------- | -----------
country | The country the venue is in
state | The state/province the venue is in
merchant | The merchant that the venue belongs to
products | All the products offered at the venue

## Get a Specific Venue with Country and State

```shell
curl "https://app.getoccasion.com/api/v1/venues/n2hs7dh?include=country,state"
  -u "59a8517fd9458b46d4ee59f8fd717fb80d:de7b7ae9e2e9e01a9508290e599"
```

```http
HTTPS/1.1 200 OK
```

```json
{
  "data": {
    "type": "venues",
    "id": "n2hs7dh",
    "attributes": {
      "name": "The Playplace",
      "address": "123 Main Street",
      "city": "Chicago",
      "zip": "60614",
      "website": "www.example.com",
      "email": "admin@example.com",
      "capacity": 100,
      "phone": "(999) 999-9999",
      "public": "true",
      "time_zone": "America/Chicago"
    },
    "relationships": {
      "country": {
        "data": {
          "id": "012sje",
          "type": "countries"
        }
      },
      "state": {
        "data": {
          "id": "7s6a652",
          "type": "states"
        }
      }
    }
  },
  "included": [
    {
      "id": "012sje",
      "type": "countries",
      "attributes": {
        "name": "United States of America",
        "code": "USA"
      }
    },
    {
      "id": "7s6a652",
      "type": "states",
      "attributes": {
        "name": "Illinois",
        "code": "IL"
      }
    }
  ]
}
```

This endpoint retrieves a specific venue, with its country and state included. If made in a public context, only a venue `where(public: true)` can be returned.

### HTTP Request

`GET https://app.getoccasion.com/api/v1/venues/:id?include=country,state`

### URL Parameters

Parameter | Description
--------- | -----------
id | The ID of the venue to retrieve

### Response Body

Notable response fields include:

Field | Public | Description
----- | ------ | -----------
name | true | The name of the venue
address | true | The street address of the venue
city | true | The city the venue is located in
zip | true | The ZIP code of the venue
website | true | The venue's website
email | true | The email of the venue
capacity | false | The number of open orders that a venue can have for any product
phone | true | The phone number of the venue
public | false | If `false`, the venue should not be displayed as open for business
time_zone | true | The time zone that the venue operates in

### Associations

Possible associations to include are:

Association | Description
----------- | -----------
country | The country the venue is in
state | The state/province the venue is in
merchant | The merchant that the venue belongs to
products | All the products offered at the venue
