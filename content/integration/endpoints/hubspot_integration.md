---
title: HubSpot Endpoint
---

## Overview

[HubSpot](http://www.hubspot.com/) is an inbound marketing software platform that helps you track the success of your company's marketing strategy, using a variety of tools. Integration with HubSpot enables automatic creation and/or updating of existing contacts, based on orders that are created, updated, or canceled in your Spree store.

+++
The source code for the [HubSpot Endpoint](https://github.com/spree/hubspot_endpoint/) is available on Github.
+++

## Services

### Contact Import

Processes incoming orders that are new, updated, or canceled and either creates or updates the HubSpot contact that matches billing address for the order.

#### Request

---order_new.json---
```json
{
  "message": "order:new",
  "payload": {
    "order": {
      "channel": "Amazon",
      "email": "test1@test.com",
      "currency": "USD",
      "placed_on": "01/01/2013 12:34:22 UTC",
      "updated_at": "01/01/2013 12:34:22 UTC",
      "status": "complete",
      "totals": {
        "item": 12.99,
        "adjustment": 10,
        "tax": 6,
        "shipping": 4,
        "order": 29.99
      },
      "adjustments": [
        {
          "name": "Shipping Discount",
          "value": "-4.99"
        },
        {
          "name": "Promotion Discount",
          "value": "-3.00"
        }
      ],
      "line_items": [
        {
          "name": "Foo T-Shirt Size(L)",
          "sku": "ABC-123",
          "external_ref": "ABD-123",
          "name": "Foo T-Shirt Size(L)",
          "quantity": 1,
          "price": 19.99,
          "options": {"color": "BLK", "size": "XL" }
        },
        {
          "name": "Foo Shoe",
          "sku": "DEF-123",
          "external_ref": "DDD-123",
          "name": "Foo Socks",
          "quantity": 3,
          "price": 23.99,
          "options": {"color": "BLK", "size": "XL" }
        }
      ],
      "shipping_address": {
        "firstname": "Chris",
        "lastname": "Mar",
        "address1": "112 Hula Lane",
        "address2": "",
        "city": "Leesburg",
        "zipcode": "20175",
        "phone": "555-555-1212",
        "country": "US",
        "state": "Virginia"
      },
      "billing_address": {
        "firstname": "Chris",
        "lastname": "Mar",
        "address1": "112 Billing Lane",
        "address2": "",
        "city": "Leesburg",
        "zipcode": "20175",
        "phone": "555-555-1212",
        "country": "US",
        "state": "Viriginia"
      },
      "payments": [
        {
          "amount": 29.99,
          "payment_method": "Standard"
        }
      ],
      "shipments": [
        {
          "cost": 29.99,
          "status": "ready",
          "stock_location": "PCH",
          "shipping_method": "UPS Next Day",
          "items": [
            {
              "name": "Foo T-Shirt Size(L)",
              "sku": "ABC-123",
              "external_ref": "ABD-123",
              "quantity": 1,
              "price": 19.99,              
              "options": {"color": "BLK", "size": "XL" }
            },
            {
              "name": "Foo Socks",
              "sku": "DEF-123",
              "external_ref": "DDD-123",
              "quantity": 3,
              "price": 23.99,              
              "options": {"color": "BLK", "size": "XL" }
            }
          ]
        }
      ]
    }
  }
}
```

### order:updated

This type of Message should be sent when an existing order is updated.

---order_updated.json---
```json
{
  "message": "order:update",
  "payload": {
    "order": {
      "channel": "Amazon",
      "email": "test1@test.com",
      "currency": "USD",
      "placed_on": "01/01/2013 12:34:22 UTC",
      "updated_at": "01/01/2013 12:34:22 UTC",
      "status": "complete",
      "totals": {
        "item": 12.99,
        "adjustment": 10,
        "tax": 6,
        "shipping": 4,
        "order": 29.99
      },
      "adjustments": [
        {
          "name": "Shipping Discount",
          "value": "-4.99"
        },
        {
          "name": "Promotion Discount",
          "value": "-3.00"
        }
      ],
      "line_items": [
        {
          "name": "Foo T-Shirt Size(L)",
          "sku": "ABC-123",
          "external_ref": "ABD-123",
          "name": "Foo T-Shirt Size(L)",
          "quantity": 1,
          "price": 19.99,
          "options": {"color": "BLK", "size": "XL" }
        },
        {
          "name": "Foo Shoe",
          "sku": "DEF-123",
          "external_ref": "DDD-123",
          "name": "Foo Socks",
          "quantity": 3,
          "price": 23.99,
          "options": {"color": "BLK", "size": "XL" }
        }
      ],
      "shipping_address": {
        "firstname": "Chris",
        "lastname": "Mar",
        "address1": "112 Hula Lane",
        "address2": "",
        "city": "Leesburg",
        "zipcode": "20175",
        "phone": "555-555-1212",
        "country": "US",
        "state": "Virginia"
      },
      "billing_address": {
        "firstname": "Chris",
        "lastname": "Mar",
        "address1": "112 Billing Lane",
        "address2": "",
        "city": "Leesburg",
        "zipcode": "20175",
        "phone": "555-555-1212",
        "country": "US",
        "state": "Viriginia"
      },
      "payments": [
        {
          "amount": 29.99,
          "payment_method": "Standard"
        }
      ],
      "shipments": [
        {
          "cost": 29.99,
          "status": "ready",
          "stock_location": "PCH",
          "shipping_method": "UPS Next Day",
          "items": [
            {
              "name": "Foo T-Shirt Size(L)",
              "sku": "ABC-123",
              "external_ref": "ABD-123",
              "quantity": 1,
              "price": 19.99,              
              "options": {"color": "BLK", "size": "XL" }
            },
            {
              "name": "Foo Socks",
              "sku": "DEF-123",
              "external_ref": "DDD-123",
              "quantity": 3,
              "price": 23.99,              
              "options": {"color": "BLK", "size": "XL" }
            }
          ]
        }
      ]
    },
    "original": {
      ... # Any custom values would be here.
    }
    "previous": {
      ... # Similar format to the "order" key.
    },
    "diff": {
      ... # Shows the difference between previous (first value in the array) and the udpated (second value in the array) orders.
    }
  }
}
```

### order:canceled

You should send this type of Message whenever an order is canceled, whether by the customer or by a store administrator.

---order_canceled.json---
```json
{
  "message": "order:canceled",
  "payload": {
    "order": {
      "channel": "Amazon",
      "email": "test1@test.com",
      "currency": "USD",
      "placed_on": "01/01/2013 12:34:22 UTC",
      "updated_at": "01/01/2013 12:34:22 UTC",
      "status": "complete",
      "totals": {
        "item": 12.99,
        "adjustment": 10,
        "tax": 6,
        "shipping": 4,
        "order": 29.99
      },
      "adjustments": [
        {
          "name": "Shipping Discount",
          "value": "-4.99"
        },
        {
          "name": "Promotion Discount",
          "value": "-3.00"
        }
      ],
      "line_items": [
        {
          "name": "Foo T-Shirt Size(L)",
          "sku": "ABC-123",
          "external_ref": "ABD-123",
          "name": "Foo T-Shirt Size(L)",
          "quantity": 1,
          "price": 19.99,
          "options": {"color": "BLK", "size": "XL" }
        },
        {
          "name": "Foo Shoe",
          "sku": "DEF-123",
          "external_ref": "DDD-123",
          "name": "Foo Socks",
          "quantity": 3,
          "price": 23.99,
          "options": {"color": "BLK", "size": "XL" }
        }
      ],
      "shipping_address": {
        "firstname": "Chris",
        "lastname": "Mar",
        "address1": "112 Hula Lane",
        "address2": "",
        "city": "Leesburg",
        "zipcode": "20175",
        "phone": "555-555-1212",
        "country": "US",
        "state": "Virginia"
      },
      "billing_address": {
        "firstname": "Chris",
        "lastname": "Mar",
        "address1": "112 Billing Lane",
        "address2": "",
        "city": "Leesburg",
        "zipcode": "20175",
        "phone": "555-555-1212",
        "country": "US",
        "state": "Viriginia"
      },
      "payments": [
        {
          "amount": 29.99,
          "payment_method": "Standard"
        }
      ],
      "shipments": [
        {
          "cost": 29.99,
          "status": "ready",
          "stock_location": "PCH",
          "shipping_method": "UPS Next Day",
          "items": [
            {
              "name": "Foo T-Shirt Size(L)",
              "sku": "ABC-123",
              "external_ref": "ABD-123",
              "quantity": 1,
              "price": 19.99,              
              "options": {"color": "BLK", "size": "XL" }
            },
            {
              "name": "Foo Socks",
              "sku": "DEF-123",
              "external_ref": "DDD-123",
              "quantity": 3,
              "price": 23.99,              
              "options": {"color": "BLK", "size": "XL" }
            }
          ]
        }
      ]
    }
  }
}
```

#### Parameters

| Name | Value | Example |
| :----| :-----| :------ |
| hubspot.access_token | Your HubSpot OAuth Token | https://mywidgets.zendesk.com/api/v2/ |

#### Response

TODO: Add response notification format
