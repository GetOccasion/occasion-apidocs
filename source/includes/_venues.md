# Venues

## Get All Venues

> **Private call** | Example truncated for brevity.

```shell
curl "http://app.getoccasion.com/api/v1/venues"
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
    "country_id": 228,
    "state_id": 14,
    "country": {
      "id": 228,
      "name": "United States",
      "code": "US"
    },
    "state": {
      "id": 14,
      "name": "Illinois",
      "code": "IL"
    },
    "created_at": "2015-10-23T11:00:44.539-05:00",
    "updated_at": "2015-10-23T11:00:44.539-05:00",
    "time_zone": "America/Chicago",
    "name": "My Classroom",
    "email": "email@example.com",
    "address": "1111 Main Street",
    "city": "Chicago",
    "zip": "60047",
    "phone": "999-999-9999",
    "website": "www.example.com",
    "capacity": 5,
    "public": false
  }
]
```

> **Public call** | Example truncated for brevity.

```shell
curl "http://app.getoccasion.com/api/v1/venues"
  -u "59a8517fd9458b46d4ee59f8fd717fb80d:"
```

```http
HTTPS/1.1 200 OK
```

```json
[
  {
    "country_id": 228,
    "state_id": 14,
    "country": {
      "id": 228,
      "name": "United States",
      "code": "US"
    },
    "state": {
      "id": 14,
      "name": "Illinois",
      "code": "IL"
    },
    "time_zone": "America/Chicago",
    "name": "My Classroom",
    "email": "email@example.com",
    "address": "1111 Main Street",
    "city": "Chicago",
    "zip": "60047",
    "phone": "999-999-9999",
    "website": "www.example.com"
  }
]
```

This endpoint retrieves all venues. If made in a public context, only venues `where(public: true)` are returned.

### HTTP Request

`GET http://example.com/api/v1/venues`

### Response Body

Notable response fields include:

Field | Public | Description
----- | ------ | -----------
time_zone | true | The time zone that the venue operates in
name | true | The name of the venue
email | true | The email of the venue
address | true | The street address of the venue
city | true | The city the venue is located in
zip | true | The ZIP code of the venue
phone | true | The phone number of the venue
website | true | The venue's website
capacity | false | The number of open orders that a venue can have for any product
public | false | If `false`, the venue should not be displayed as open for business

### Associations

Possible associations to include are:

Association | Default | Public | Description
----------- | ------- | ------ | -----------
country | true | true | The country that the venue is located in
state | true | true | The state/province the venue is located in
products | false | true | All the products that belong to the venue
merchant | false | true | The merchant that the venue belongs to

## Get a Specific Venue

> **Private call**

```shell
curl "http://app.getoccasion.com/api/v1/venues/12"
  -u "59a8517fd9458b46d4ee59f8fd717fb80d:de7b7ae9e2e9e01a9508290e599"
```

```http
HTTPS/1.1 200 OK
```

```json
{
  "id": 1,
  "merchant_id": 10,
  "country_id": 228,
  "state_id": 14,
  "country": {
    "id": 228,
    "name": "United States",
    "code": "US"
  },
  "state": {
    "id": 14,
    "name": "Illinois",
    "code": "IL"
  },
  "created_at": "2015-10-23T11:00:44.539-05:00",
  "updated_at": "2015-10-23T11:00:44.539-05:00",
  "time_zone": "America/Chicago",
  "name": "My Classroom",
  "email": "email@example.com",
  "address": "1111 Main Street",
  "city": "Chicago",
  "zip": "60047",
  "phone": "999-999-9999",
  "website": "www.example.com",
  "capacity": 5,
  "public": false
}
```

> **Public call**

```shell
curl "http://app.getoccasion.com/api/v1/venues/12"
  -u "59a8517fd9458b46d4ee59f8fd717fb80d:"
```

```http
HTTPS/1.1 200 OK
```

```json
{
  "country_id": 228,
  "state_id": 14,
  "country": {
    "id": 228,
    "name": "United States",
    "code": "US"
  },
  "state": {
    "id": 14,
    "name": "Illinois",
    "code": "IL"
  },
  "time_zone": "America/Chicago",
  "name": "My Classroom",
  "email": "email@example.com",
  "address": "1111 Main Street",
  "city": "Chicago",
  "zip": "60047",
  "phone": "999-999-9999",
  "website": "www.example.com"
}
```

This endpoint retrieves a specific venue. If made in a public context, only a venue `where(public: true)` can be returned.

### HTTP Request

`GET http://example.com/api/v1/venues/:id`

### URL Parameters

Parameter | Description
--------- | -----------
id | The ID of the venue to retrieve

### Response Body

Notable response fields include:

Field | Public | Description
----- | ------ | -----------
time_zone | true | The time zone that the venue operates in
name | true | The name of the venue
email | true | The email of the venue
address | true | The street address of the venue
city | true | The city the venue is located in
zip | true | The ZIP code of the venue
phone | true | The phone number of the venue
website | true | The venue's website
capacity | false | The number of open orders that a venue can have for any product
public | false | If `false`, the venue should not be displayed as open for business

### Associations

Possible associations to include are:

Association | Default | Public | Description
----------- | ------- | ------ | -----------
country | true | true | The country that the venue is located in
state | true | true | The state/province the venue is located in
products | false | true | All the products that belong to the venue
merchant | false | true | The merchant that the venue belongs to
