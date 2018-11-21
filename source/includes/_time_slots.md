# Time Slots

## Get Bookable or Upcoming Time Slots For A Product

```shell
curl "https://app.getoccasion.com/api/v1/products/:id/time_slots?filter[status]=bookable&filter[last]=k182hea&page[size]=2"
  -u "59a8517fd9458b46d4ee59f8fd717fb80d:de7b7ae9e2e9e01a9508290e599"
```

```http
HTTPS/1.1 200 OK
```

```json
{
  "data": [
    {
      "type": "time_slots",
      "id": "38asnd2",
      "attributes": {
        "starts_at": "2015-10-23T11:00:44.539-05:00",
        "duration": "3200",
        "spots_available": 2
      }
    },
    {
      "type": "time_slots",
      "id": "j1267fas",
      "attributes": {
        "starts_at": "2015-10-24T11:00:44.539-05:00",
        "duration": "7200",
        "spots_available": null
      }
    }
  ],
  "links": {
    "next": "https://app.getoccasion.com/api/v1/products/:id/time_slots?filter[status]=bookable&filter[last]=j1267fas&page[size]=2"
  }
}
```

This endpoint retrieves time slots for a product.

### HTTP Request

`GET https://app.getoccasion.com/api/v1/products/:id/time_slots?filter[status]=bookable&filter[last]=k182hea&page[size]=2`

### URL Parameters

Parameter | Description | Required
--------- | ----------- | ---------
id | The ID of the product to retrieve time slots for. | true
filter | The filter params to apply to collection of time slots for the product. | true
&#x203a; last | The token of the last time slot that was in your previous time slot query. If left blank, will respond with first upcoming time slots. | false
&#x203a; status | The status type of time slot to respond with. Only `bookable` or `upcoming` are supported. `bookable` returns all bookable time slots, and `upcoming` also includes time slots that are sold out. | true
page | The pagination params to apply to collection of time slots for the product. | false
&#x203a; size | The number of time slots to respond with. Defaults to 10, max 100. | false

### Response Body

Notable response fields include:

Field | Public | Description
----- | ------ | -----------
starts_at | true | The time that the time slot starts at.
duration | true | The duration of the time slot, in seconds.
spots_available | true | The number of spots available for purchase for this time slot. If `null`, unlimited spots available.
