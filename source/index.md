---
title: API Reference

language_tabs:
  - shell
  - python

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='http://github.com/tripit/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introduction

Fulfil.IO is software to track your inventory, whether you sell 
online, offline or through a third party like Shopify.

## What can I do with this API ?

Everything :-)

Any operation that can be done by an user can be done through our
API. If you are not able to figure out a way of doing it do get in
touch with our team and we will help you.

## Why should I use this API ?

Some common use cases:

1. You have an order system like an e-commerce engine (shopify, 
   magento, prestashop) and you want to integrate with Fulfil.IO
   for fulfilling those orders.
2. You have a point of sale system and you want to know the
   inventory from Fulfil.IO.
3. Creating products, managing catalogs, so on and so forth.
4. Dashboards, reports.


## Test API Connection

> To authorize, use this code:

```python
import requests

requests.get(
    'https://demo.fulfil.io/api/v1/test',
    auth=('APIKEY', None)
).json()
```

```shell
# With shell, you can just pass the APIKEY as basic auth username
curl "https://demo.fulfil.io/api/v1/test"
  -u APIKEY:
```

> The above command returns JSON structured like this:

```json
{
  "message": "Special cases aren't special enough to break the rules.",
  "success": true
}
```

A convenient way to test if your source code is working is by
calling the `/test` endpoint, which returns a success flag and
a useful message from the zen of python.

<aside class="notice">
Make sure to replace `APIKEY` with your API key.
</aside>

## Authentication

You need to [generate an API key](https://fulfilio.zendesk.com/hc/en-us/articles/213488947-Creating-API-Tokens)
for your username first.
You should be able to do this from User Preferences menu or
you can generate it from your Users menu. (Access to the
users menu is limited to administrators.)

`Authorization: Basic base64-encoded-api-key`

<aside class="notice">
You must replace <code>base64-encoded-api-key</code> with your base64 encoded API key.
</aside>

## Common fields on all records

All records have some metadata that is common.

Field Name | Description
----------  ------------
create_uid | ID of the use who created the record
create_date| The UTC timestamp at which the record was created
write_uid | ID of the use who last edited the record (could be null if record was never edited)
write_date| The UTC timestamp at which the record was last modified. (could be null)

# Contacts

## Get All Parties

```python
import requests

response = requests.get(
    'https://demo.fulfil.io/api/v1/model/party.party',
    auth=('APIKEY', None)
)
response.json()
```

```shell
curl "https://demo.fulfil.io/api/v1/model/party.party"
  -u APIKEY:
```

> The above command returns JSON structured like this:

```json
[
  {"rec_name": "ABC Inc.", "id": 1},
  {"rec_name": "Daniel Craig", "id": 2},
  {"rec_name": "Sharoon Thomas", "id": 3}
]
```

This endpoint retrieves all parties.

### HTTP Request

`GET https://demo.fulfil.io/api/v1/model/party.party`

### Filter the list

`GET https://demo.fulfil.io/api/v1/model/party.party?domain=[['name', 'ilike', '%daniel%']]`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
page | 1 | Select the page when there are more records
per_page | 10 | The number of results per page. Larger the number, slower the response


## Create a new party

```python
import requests

response = requests.post(
    'https://demo.fulfil.io/api/v1/model/party.party',
    auth=('APIKEY', None),
    json=[{'name': 'New party'}]
)
response.json()
```

```shell
curl \
    -H "Content-Type: application/json" \
    -X POST \
    -d '[{"name": "New party"}]' \
    -u APIKEY: \
    https://demo.fulfil.io/api/v1/model/party.party
```

> The above command returns JSON structured like this:

```json
[{"rec_name": "New party", "id": 3}]
```

## Get a Specific Party


```python
import requests

response = requests.get(
    'https://demo.fulfil.io/api/v1/model/party.party/1',
    auth=('APIKEY', None)
)
response.json()
```

```shell
curl "https://demo.fulfil.io/api/v1/model/party.party/1"
  -u APIKEY:
```

> The above command returns JSON structured like this:

```json
{
  "name": "Fulfil.IO INC",
  "code": "1",
  "active": true,
  "lang": null,

  # Computed information for quick access
  # You cannot write to these fields
  "rec_name": "Fulfil.IO INC",
  "full_name": "Fulfil.IO INC",
  "website": "",
  "fax": "",
  "phone": "",
  "mobile": "",
  "email": "",

  # Classification/Categorization
  "categories": [],

  # VAT details (EU)
  "vat_number": "",
  "vat_code": "",
  "vat_country": null,

  # ID of addresses
  "addresses": [1],

  # Stored payment profiles (Credit Cards/Bank Accounts)
  "default_payment_profile": null,
  "payment_profiles": [],

  # Fields common to all records (metadata)
  "id": 1,
  "create_uid": 1,
  "write_uid": null,
  "create_date": {
    "second": 49,
    "microsecond": 705297,
    "minute": 59,
    "hour": 15,
    "year": 2015,
    "__class__": "datetime",
    "day": 28,
    "month": 10
  },
  "write_date": null,

  "channel": null,
  "contact_mechanisms": [],

  # Sale defaults
  "sale_price_list": null,
  "customer_tax_rule": null,
  "customer_payment_term": null,
  "supplier_location": 5,
  "customer_location": 6,
  "sale_shipment_grouping_method": "standard",

  # Purchase defaults
  "supplier_tax_rule": null,
  "supplier_payment_term": null,

  # Channel mappings
  "ebay_user_id": "",
  "prestashop_id": null,
  "amazon_user_email": null,
  "magento_ids": [],

  # GL/Accounts for receivable and payable
  "account_payable": 4,
  "account_receivable": 5,

  # AR and AP balances.
  "payable_today": {
    "decimal": "0.0",
    "__class__": "Decimal"
  },
  "payable": {
    "decimal": "0.0",
    "__class__": "Decimal"
  },
  "receivable": {
    "decimal": "0.0",
    "__class__": "Decimal"
  },
  "receivable_today": {
    "decimal": "0.0",
    "__class__": "Decimal"
  },

  "nereid_session": null,
  "nereid_users": [],
}
```

This endpoint retrieves a specific party.


### HTTP Request

`GET https://demo.fulfil.io/api/v1/model/party.party/<ID>`

### HTTP Request with selected fields

`GET https://demo.fulfil.io/api/v1/model/party.party/<ID>?field=name&field=code`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the party to retrieve
field | Name of additional fields to fetch

# Shipments

## Get all customer shipments

```python
import requests

response = requests.get(
    'https://demo.fulfil.io/api/v1/model/stock.shipment.out',
    auth=('APIKEY', None)
)
response.json()
```

```shell
curl "https://demo.fulfil.io/api/v1/model/stock.shipment.out"
  -u APIKEY:
```

> The above command returns JSON structured like this:

```json
[
  {"rec_name": "ABC Inc.", "id": 1},
]
```

This endpoint retrieves all customer shipments.

### HTTP Request

`GET https://demo.fulfil.io/api/v1/model/stock.shipment.out`

### Filter the list for shipments in a specific state

`GET https://demo.fulfil.io/api/v1/model/stock.shipment.out?domain=[['state', '=', 'waiting']]`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
page | 1 | Select the page when there are more records
per_page | 10 | The number of results per page. Larger the number, slower the response

### States of a customer shipment

State | Description
----- | -----------
draft | A draft shipment. (Default)
waiting | Waiting to be allocated inventory.
assigned | Inventory has been allocated to the order
packed | The package has been made
done | The shipment is completed for carrier to pick up

## Create a new shipment

```python
import requests

data = [
    {
        "customer": 2,
        "delivery_address": 4
    }
]
response = requests.post(
    'https://demo.fulfil.io/api/v1/model/stock.shipment.out',
    json=data,
    auth=('APIKEY', None)
)
response.json()
```

```shell
curl \
    -H "Content-Type: application/json" \
    -X POST \
    -d '[{"customer": 1}]' \
    -u APIKEY: \
    https://demo.fulfil.io/api/v1/model/stock.shipment.out
```


### Fields in customer shipment

Field Name | Description | Required | Type
-----------|-------------|----------|-------
customer | ID of the party to which the shipment is sent to | yes | Integer ID
delivery_address | The ID of the address to which the shipment is being sent. | yes | Integer ID
code | A number for the shipment | no (automatically assigned) | String
reference | Your reference for the shipment. Usually used for order number | no | String
warehouse | The warehouse from which the shipment should be shipped | no (if only 1 warehouse) | Integer ID
shipping_instructions | Instruction to print on picking list | no | Text
company | ID of the company | no (if only 1 company) | Integer ID
tracking_number | The tracking number of the shipment | no | Char

## Get a specific shipment

```python
import requests

response = requests.get(
    'https://demo.fulfil.io/api/v1/model/stock.shipment.out/1',
    auth=('APIKEY', None)
)
response.json()
```

```shell
curl "https://demo.fulfil.io/api/v1/model/stock.shipment.out/1"
  -u APIKEY:
```

> The above command returns JSON structured like this:

```json
{
  "code": "3",
  "customer": 1,
  "delivery_address": 1,
  "reference": null,
  "warehouse": 4,
  "shipping_instructions": null,
  "company": 1,

  # Shipping and carrier
  "carrier": null,
  "tracking_number": null,

  "priority": null,
  "planned_date": null,
  "effective_date": null,

  # Fields common to all records (metadata)
  "id": 1,
  "create_uid": 1,
  "write_uid": null,
  "create_date": {
    "second": 49,
    "microsecond": 705297,
    "minute": 59,
    "hour": 15,
    "year": 2015,
    "__class__": "datetime",
    "day": 28,
    "month": 10
  },
  "write_date": null,

  "root_packages": [
    
  ],
  "sales": [
    
  ],

  "warehouse_storage": 3,
  "warehouse_output": 2,
  "customer_location": 6,

  "moves": [],
  "outgoing_moves": [],
  "inventory_moves": [],

  # Packages: USefyl
  "packages": [],

  # Status of the shipment
  "state": "draft",
}
```

## Creating a new shipment (with lines)

```python
import requests

auth = ('APIKEY', None)

customer = requests.get(
    "https://demo.fulfil.io/api/v1/model/party.party/1",
    auth=auth
).json()

product1 = requests.get(
    "https://demo.fulfil.io/api/v1/model/product.product/1",
    auth=auth
).json()

customer_location = requests.get(
    'https://demo.fulfil.io/api/v1/model/stock.location?domain=[["code", "=", "CUS"]]',
    auth=auth
).json()[0]
output_location = requests.get(
    'https://demo.fulfil.io/api/v1/model/stock.location?domain=[["code", "=", "OUT"]]',
    auth=auth
).json()[0]

data = [
    {
        "customer": customer["id"],
        "delivery_address": customer["addresses"][0],
        "outgoing_moves": [['create', [{
            "product": product1["id"],
            "quantity": 10,
            "uom": product1["default_uom"],
            "to_location": customer_location["id"],
            "from_location": output_location["id"],
            "unit_price": {
                "decimal": "200.00",
                "__class__": "Decimal",
            }
        }]]]
    }
]
response = requests.post(
    'https://demo.fulfil.io/api/v1/model/stock.shipment.out',
    json=data,
    auth=auth
)
response.json()
```
