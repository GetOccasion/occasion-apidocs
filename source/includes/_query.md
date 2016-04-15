# Query Interface

## Filtering

```shell
curl "http://app.getoccasion.com/api/v1/products?venue_id=10"
  -u "59a8517fd9458b46d4ee59f8fd717fb80d:de7b7ae9e2e9e01a9508290e599"
```

> Only products with venue_id=10 will be rendered in the response.

Attaching any field/value pair of a record as a query parameter will allow you to filter the response by that field, responding only with records that meet your conditions.

### URL Parameters

Parameter | Default | Description
---------- | ------- | ----------
[field_name]<br>*optional* | none | The field to filter records by

## Sorting

```shell
curl "http://app.getoccasion.com/api/v1/products?sort=updated_at"
  -u "59a8517fd9458b46d4ee59f8fd717fb80d:de7b7ae9e2e9e01a9508290e599"
```

> Products will be sorted in ascending updated_at order.

```shell
curl "http://app.getoccasion.com/api/v1/products?sort=-updated_at,title"
  -u "59a8517fd9458b46d4ee59f8fd717fb80d:de7b7ae9e2e9e01a9508290e599"
```

> Products will be sorted in descending updated_at order, then ascending title order

Specifying a `sort` parameter in your query will respond with the collection sorted by your specified field, in ascending order. Attaching a `-` sign in front of the value will sort in descending order.

### URL Parameters

Parameter | Default | Description
---------- | ------- | ----------
sort<br>*optional* | id | The fields to sort by

## Pagination

```shell
curl "http://app.getoccasion.com/api/v1/products?per_page=5&page=1"
  -u "59a8517fd9458b46d4ee59f8fd717fb80d:de7b7ae9e2e9e01a9508290e599"
```

> Products will be paginated in groups of 5, with the second page rendered as the response.

Specifying pagination params `page` and `per_page` allow you to paginate the response of the collection you are querying.

### URL Parameters

Parameter | Default | Description
---------- | ------- | ----------
per_page<br>*optional* | 10 | The number of records per page
page<br>*optional* | 0 | Which page of records to respond with

## Fields

```shell
curl "http://app.getoccasion.com/api/v1/products?fields=title,description"
  -u "59a8517fd9458b46d4ee59f8fd717fb80d:de7b7ae9e2e9e01a9508290e599"
```

> Products will only be rendered with their title and description fields.

Specifying `fields` query parameters will only render those fields of the records in the response.

### URL Parameters

Parameter | Default | Description
---------- | ------- | ----------
fields<br>*optional* | all fields | The fields to render in the response

## Include

```shell
curl "http://app.getoccasion.com/api/v1/products?include=merchant,venue"
  -u "59a8517fd9458b46d4ee59f8fd717fb80d:de7b7ae9e2e9e01a9508290e599"
```

> Products will be rendered with their merchant and venue associated records included. *Example truncated for brevity.*

```http
HTTPS/1.1 200 OK
```
```json
[
  {
    "id": 1,
    "merchant_id": 10,
    "venue_id": 15,
    "merchant": {
      "id": 10,
      "name": "A Business"
    },
    "venue": {
      "id": 15,
      "name": "Our Location"
    }
  }
]
```

Specifying `include` query parameters will render associations of records in the response body of each record.

### URL Parameters

Parameter | Default | Description
---------- | ------- | ----------
include<br>*optional* | varies by record model | The associations to include in the response
