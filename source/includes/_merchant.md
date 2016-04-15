# Merchant

> **Private call**

```shell
curl "http://app.getoccasion.com/api/v1/merchant"
  -u "59a8517fd9458b46d4ee59f8fd717fb80d:de7b7ae9e2e9e01a9508290e599"
```

```http
HTTPS/1.1 200 OK
```

```json
{
  "id": 1,
  "profile_picture": "Logo.jpg",
  "created_at": "2015-10-23T11:00:44.539-05:00",
  "updated_at": "2015-10-23T11:00:44.539-05:00",
  "name": "My Business Name",
  "net_balance": "12000.0",
  "time_zone": "America/Chicago",
  "business_type": "Skate Rink",
  "paying": true,
  "tax_percentage": "2.0",
  "free_trial_ends_at_date": "2015-10-23T11:00:44.539-05:00",
  "free_trial_volume": "1000.0",
  "free_trial_days_left": "15",
  "free_trial_volume_left": "500.0",
  "send_weekly_sales_email": true,
  "send_reminder_email": true,
  "facebook_page": "https://www.facebook.com/xxxx?fref=ts",
  "psp_id": 1,
  "psp": {
    "id": 1,
    "name": "SpreedlyPsp",
    "payment_description": "Credit Card",
    "can_refund": true
  },
  "currency": {
    "id": 1,
    "name": "USD",
    "code": "$"
  }
}
```

> **Public call**

```shell
curl "http://app.getoccasion.com/api/v1/products"
  -u "59a8517fd9458b46d4ee59f8fd717fb80d:"
```

```http
HTTPS/1.1 200 OK
```

```json
{
  "profile_picture": "Logo.jpg",
  "name": "My Business Name",
  "time_zone": "America/Chicago",
  "tax_percentage": "2.0",
  "facebook_page": "https://www.facebook.com/xxxx?fref=ts",
  "currency": {
    "id": 1,
    "name": "USD",
    "code": "$"
  }
}
```

This endpoint retrieves the merchant corresponding to your provided API credentials.

### HTTP Request

`GET http://example.com/api/v1/merchant`

### Response Body

Notable response fields include:

Field | Public | Description
----- | ------ | -----------
profile_picture | true | The URL for the merchant's logo image
name | true | The name of the business
net_balance | false |The sum of the amounts of all cashable transactions minus the operator fees, i.e. how much money can be withdrawn to a bank account
time_zone | true | The timezone that the merchant operates in
business_type | false | The type of business that the merchant operates: `'Art Studio'`, `'Dance Studio'`, etc.
paying | false | Whether or not the merchant is paying for Occasion
tax_percentage | true | The sales tax percentage that the merchant applies to each order subtotal
free_trial_ends_at_date | false | The date after which the merchant must start paying to use Occasion
free_trial_volume | false | The sales volume that a merchant is allowed to reach before they must start paying to use Occasion
free_trial_days_left | false | The number of days left until the merchant must pay to continue using Occasion
free_trial_volume_left | false | The sales volume remaining before a merchant must pay to continue using Occasion
send_weekly_sales_email | false | If `true`, merchant will receive a weekly email summarizing their order sales
send_reminder_email | false | If `true`, merchant will send out a reminder email to customers 3 days before their booked event
facebook_page | true | The Facebook page URL for the merchant's business
psp | false | The payment service provider that the merchant uses to process payments
&#x25B8; name | | The name of the PSP.<br><br>*Possible values:* `"Cash"`,`"SpreedlyPsp"`,<br>`"QantaniIdeal"`
&#x25B8; payment_description | | The description of how payments are processed.<br><br>*Possible values:*<br>`"Cash"` - Merchant only accepts cash<br>`"Credit Card"` - Merchant accepts credit cards/Paypal/eCheck<br>`"iDEAL"` - Merchant accepts bank accounts through iDEAL network
&#x25B8; can_refund | | Whether or not the merchant can refund transactions with this PSP.

### Associations

Possible associations to include are:

Association | Default | Public | Description
----------- | ------- | ------ | -----------
psp | true | false | The payment service provider that the merchant uses to process payments
currency | true | true | The currency that the merchant accepts
