# Query Interface

## Filtering

```shell
curl "http://app.getoccasion.com/api/v1/products?filter[price]=5"
  -u "59a8517fd9458b46d4ee59f8fd717fb80d:de7b7ae9e2e9e01a9508290e599"
```

> Only products with price=5 will be rendered in the response.

Attaching any field/value pair of a record as a filter query parameter will allow you to filter the response by that field, responding only with records that meet your conditions.

### URL Parameters

Parameter | Default | Description
---------- | ------- | ----------
filter[field_name]<br>*optional* | none | The field to filter records by

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
sort<br>*optional* | -created_at | The fields to sort by

## Pagination

```shell
curl "http://app.getoccasion.com/api/v1/products?page[size]=5&page[number]=1"
  -u "59a8517fd9458b46d4ee59f8fd717fb80d:de7b7ae9e2e9e01a9508290e599"
```

> Products will be paginated in groups of 5, with the second page rendered as the response.

Specifying pagination params `page[size]` and `page[number]` allows you to paginate the response of the collection you are querying.

### URL Parameters

Parameter | Default | Description
---------- | ------- | ----------
page[size]<br>*optional* | 50 | The number of records per page
page[number]<br>*optional* | 1 | Which page of records to respond with

## Fields

```shell
curl "http://app.getoccasion.com/api/v1/products?fields[products]=title,description"
  -u "59a8517fd9458b46d4ee59f8fd717fb80d:de7b7ae9e2e9e01a9508290e599"
```

> Products will only be rendered with their title and description fields.

Specifying `fields` query parameters will only render those fields of the records in the response.

### URL Parameters

Parameter | Default | Description
---------- | ------- | ----------
fields<br>*optional* | all fields (public or private) | The fields to render in the response

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
{
  "data": [
    {  
      "type": "products",
      "id": "asdj38",
      "attributes": {
        "title": "A product title",
        "description": "A product description"
      },
      "relationships": {
        "merchant": {
          "data": {
            "type": "merchants",
            "id": "lhj8we"
          }
        },
        "venue": {
          "data": {
            "type": "venues",
            "id": "jk47sh"
          }
        }
      }
    }
  ],
  "included": [
    {
      "type": "merchants",
      "id": "lhj8we",
      "attributes": {
        "name": "A Business name"
      }
    },
    {
      "type": "venues",
      "id": "jk47sh",
      "attributes": {
        "name": "Our Business Location"
      }
    }
  ]
}
```

Specifying `include` query parameters will render associations of records in the response body of each record.

### URL Parameters

Parameter | Default | Description
---------- | ------- | ----------
include<br>*optional* | none | The associations to include in the response

## More Details on Modifying Query

To best understand the full power of the JSON API query interface, [read the docs for it](http://jsonapi.org/format/#fetching).
