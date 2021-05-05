---
title: Invoices
layout: default
---

# Invoices

--- row ---

**Invoice attributes**

{:.table}
| field                | type    | description                                 |
| -------------------  | ------- | ------------------------------------------- |
| id                   | string  | unique ID                                   |
| total_price          | integer | price of this invoice (cents)               |
| total_price_with_vat | integer | price of this invoice including VAT (cents) |
| billing_month        | date    | this invoice is related to this month       |
| pdf_url              | string  | URL to download the PDF invoice             |
| invoice_number       | string  | the invoice number                          |
| state                | string  | state of this invoice (new, paid or failed) |
| vat_rate             | integer | the VAT rate applied to this invoice (in ‰) |
| items                | array   | the list of item to pay, present on the doc |
| detailed_items       | array   | detail breakdown of the consumption         |


**Invoice Item attributes**

{:.table}
| field      | type    | description                                         |
| ---------  | ------- | --------------------------------------------------- |
| id         | string  | unique ID                                           |
| label      | string  | label of the invoice entry                          |
| price      | integer | price of the item (cents)                           |
| app        | string  | (detailed items only) name of the app               |
| duration   | integer | (detailed items only) minutes charged for this item |

||| col |||

Example object:

```json
{
	"invoice": {
		"id": "23d2c27f-bac0-4038-b3d7-2e6f06f3d27a",
		"total_price": 0,
		"total_price_with_vat": 0,
		"billing_month": "2020-08-01",
		"pdf_url": "https://download.scalingo.com/invoices/23d2c27f-bac0-4038-b3d7-2e6f06f3d27a/download",
		"invoice_number": "2020-09-1442",
		"state": "paid",
		"vat_rate": 200,
		"items": [
			{
				"id": "57c826d022fcfa0012ae9ae9",
				"label": "Containers Runtime",
				"price": 2200
			},
			{
				"id": "57c826d022fcfa0012ae9aea",
				"label": "Addons",
				"price": 0
			},
			{
				"id": "57c826d022fcfa0012ae9aeb",
				"label": "Free Trial 2020-06-02 15:07 -> 2020-09-30 15:07",
				"price": -2200
			}
		],
		"detailed_items": [
			{
				"id": "57c826d022fcfa0012ae9aec",
				"label": "Containers - type: web- size: M",
				"price": 0,
        "duration": 0,
				"app": "example-app"
			},
			{
				"id": "57c826d022fcfa0012ae9aed",
				"label": "Containers - type: web- size: S",
				"price": 725,
        "duration": 43200,
				"app": "example-app"
			},
			// …
		]
	}
}
```

--- row ---

## List Your Invoices

`GET https://$SCALINGO_API_URL/v1/account/invoices`

List all your invoices.

||| col |||

Example

```shell
curl -H "Accept: application/json" -H "Content-Type: application/json" \
  -H "Authorization: Bearer $BEARER_TOKEN" \
  -X GET https://$SCALINGO_API_URL/v1/account/invoices
```

Returns 200 OK

```json
{
	"invoices": [
		{
			"id": "23d2c27f-bac0-4038-b3d7-2e6f06f3d27a",
			"total_price": 0,
			"total_price_with_vat": 0,
			"billing_month": "2020-08-01",
			"pdf_url": "https://download.scalingo.com/invoices/23d2c27f-bac0-4038-b3d7-2e6f06f3d27a/download",
			"invoice_number": "2020-09-1442",
			"state": "paid",
			"vat_rate": 200,
			"items": [
				{
					"id": "57c826d022fcfa0012ae9ae9",
					"label": "Containers Runtime",
					"price": 2200
				},
				{
					"id": "57c826d022fcfa0012ae9aea",
					"label": "Addons",
					"price": 0
				},
				{
					"id": "57c826d022fcfa0012ae9aeb",
					"label": "Free Trial 2020-06-02 15:07 -> 2020-09-30 15:07",
					"price": -2200
				}
			],
			"detailed_items": [
				{
					"id": "57c826d022fcfa0012ae9aec",
					"label": "Containers - type: web- size: M",
					"price": 0,
					"app": "example-app"
				},
				{
					"id": "57c826d022fcfa0012ae9aed",
					"label": "Containers - type: web- size: S",
					"price": 725,
					"app": "example-app"
				},
				// …
			]
		},
		{
			// …
		}
	],
	"meta": {
		"pagination": {
			"current_page": 1,
			"next_page": null,
			"previous_page": null,
			"total_pages": 1,
			"total_count": 2
		}
	}
}
```

--- row ---

## Get a Precise Invoice

--- row ---

`GET https://$SCALINGO_API_URL/v1/account/invoices/[:invoice_id]`

Display a precise invoice

||| col |||

Example request

```shell
curl -H "Accept: application/json" -H "Content-Type: application/json" \
  -H "Authorization: Bearer $BEARER_TOKEN" \
  -X GET https://$SCALINGO_API_URL/v1/account/invoices/23d2c27f-bab0-4038-b3d7-2e6f06f3d27a
```

Returns 200 OK

```json
{
	"invoice": {
		"id": "23d2c27f-bac0-4038-b3d7-2e6f06f3d27a",
		"total_price": 0,
		"total_price_with_vat": 0,
		"billing_month": "2020-08-01",
		"pdf_url": "https://download.scalingo.com/invoices/23d2c27f-bac0-4038-b3d7-2e6f06f3d27a/download",
		"invoice_number": "2020-09-1442",
		"state": "paid",
		"vat_rate": 200,
		"items": [
			{
				"id": "57c826d022fcfa0012ae9ae9",
				"label": "Containers Runtime",
				"price": 2200
			},
			{
				"id": "57c826d022fcfa0012ae9aea",
				"label": "Addons",
				"price": 0
			},
			{
				"id": "57c826d022fcfa0012ae9aeb",
				"label": "Free Trial 2020-06-02 15:07 -> 2020-09-30 15:07",
				"price": -2200
			}
		],
		"detailed_items": [
			{
				"id": "57c826d022fcfa0012ae9aec",
				"label": "Containers - type: web- size: M",
				"price": 0,
				"app": "example-app"
			},
			{
				"id": "57c826d022fcfa0012ae9aed",
				"label": "Containers - type: web- size: S",
				"price": 725,
				"app": "example-app"
			},
			// …
		]
	}
}
```

--- row ---

## Download a Precise Invoice

--- row ---

`GET https://$SCALINGO_API_URL/v1/account/invoices/[:invoice_id]/download`

This request downloads the invoice's PDF.

||| col |||

Example request

```sh
curl -H "Accept: application/pdf,application/json" \
  -H "Authorization: Bearer $BEARER_TOKEN" \
  -X GET 'https://$SCALINGO_API_URL/v1/account/invoices/23d2c27f-bac0-4038-b3d7-2e6f06f3d27a/download'
```

Returns 302 Found
