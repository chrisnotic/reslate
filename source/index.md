---
title: API reference

language_tabs: # must be one of https://prismjs.com/#supported-languages
  - shell

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/slatedocs/slate'>Documentation Powered by Slate</a>

includes:

search: true
code_clipboard: true
---

# Introduction

Welcome to Freddy's Artisinal Halloween Candy Shop API. Through this API, you can log in to the store and retrieve data on the store's products, sales numbers, and order history.

# Authentication

API requests are authenticated by a JSON web token (JWT). Log in through the [login endpoint](#login) to receive your access token. Pass the access token in the header as a `Bearer Token` when making requests to the [dashboard](#retrieve-dashboard-information) or [order history](#retrieve-order-history) endpoints.

```shell
# Pass the authentication header with each request
curl https://freddy.codesubmit.io/ \
-H "Authorization: Bearer {access_token}"
```

> Make sure to replace `{access_token}` with your live access token.

Pass your access token in a header using this format:

`Authorization: Bearer {access_token}`

<aside class="notice">
You must replace <code>{access_token}</code> with your personal access token.
</aside>

## Login

```shell
curl https://freddy.codesubmit.io/login \
-X POST \
-H "Content-Type: application/json" \
-d '{"username":"freddy","password":"ElmStreet2019"}'
```

> In the response, you will receive your `access_token` and `refresh_token`:

```json
{
  "access_token": "{access_token}",
  "refresh_token": "{refresh_token}"
}
```

Log in through this endpoint to retrieve your `access_token` and `refresh_token`. Use your `access_token` to authenticate on the [dashboard](#retrieve-dashboard-information) and [order history](#retrieve-order-history) endpoints.

Your `access_token` is valid for 15 minutes after generation. You can refresh it any time by passing your `refresh_token` to the [refresh endpoint](#refresh-access-token). You will receive a new `access_token` in the response. Your `refresh_token` is valid for 30 days after generation.

### Endpoint

`POST https://freddy.codesubmit.io/login`

### Body parameters

Parameter | Description
--------- | -----------
`username` | Your Freddy's Artisinal Halloween Candy Shop account username
`password` | Your Freddy's Artisinal Halloween Candy Shop account password 

## Refresh access token

```shell
curl https:/freddy.codesubmit.io/refresh \
-X POST \
-H "Authorization: Bearer {refresh_token}"
```

> The response provides a new `access_token` that you can use on the [dashboard](#retrieve-dashboard-information) and [order history](#retrieve-order-history) endpoints:

```json
{
  "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpYXQiOjE2MTE1ODk1MTUsIm5iZiI6MTYxMTU4OTUxNSwianRpIjoiYzkyYzJhMzUtMDc3Mi00NDc3LTg0OTAtYTQzMTc0OWMzYzY3IiwiZXhwIjoxNjExNTkwNDE1LCJpZGVudGl0eSI6ImZyZWRkeSIsImZyZXNoIjpmYWxzZSwidHlwZSI6ImFjY2VzcyJ9.nn8az_xc7y4bw5uaqfFKzgbcAAxF0DZlUcDnMy8-Z6Q"
}
```

Refresh your `access_token` using this endpoint. You can refresh your `access_token` at any time for 30 days after you first [log in](#login). Each `access_token` is valid for 15 minutes.

### Endpoint

`POST https:/freddy.codesubmit.io/refresh`

# Dashboard

## The dashboard object

> 

```json
{
  "bestsellers": [
    {
      "product": {
        "id": "e2414f21-2647-c4aa-748a-81dc838db74a",
        "image": "https://images.unsplash.com/photo-1463860914822-61dc3ee606f7?crop=entropy&cs=tinysrgb&fit=crop&fm=jpg&h=500&ixid=eyJhcHBfaWQiOjF9&ixlib=rb-1.2.1&q=80&w=500",
        "name": "Cartoon Network Studios Lime Flower Youngberry Gummies"
      },
      "revenue": 2835702,
      "units": 6178
    },
    {
      "product": {
        "id": "99564712-9bb0-fc90-aae4-5d7dcc6dd35a",
        "image": "https://images.unsplash.com/photo-1463860914822-61dc3ee606f7?crop=entropy&cs=tinysrgb&fit=crop&fm=jpg&h=500&ixid=eyJhcHBfaWQiOjF9&ixlib=rb-1.2.1&q=80&w=500",
        "name": "Magik Lamp Jasmine Flowers Cowberry Drops"
      },
      "revenue": 1798368,
      "units": 4323
    },
    {
      "product": {
        "id": "54cde370-ebf7-2895-113d-0c327c11d97a",
        "image": "https://images.unsplash.com/photo-1463860914822-61dc3ee606f7?crop=entropy&cs=tinysrgb&fit=crop&fm=jpg&h=500&ixid=eyJhcHBfaWQiOjF9&ixlib=rb-1.2.1&q=80&w=500",
        "name": "Profitpros Licorice, Liquorice Cocky Apple Snack"
      },
      "revenue": 3665331,
      "units": 3669
    },
    {
      "product": {
        "id": "07f4f715-b8c5-a308-0cbf-49fe627a8d59",
        "image": "https://images.unsplash.com/photo-1463860914822-61dc3ee606f7?crop=entropy&cs=tinysrgb&fit=crop&fm=jpg&h=500&ixid=eyJhcHBfaWQiOjF9&ixlib=rb-1.2.1&q=80&w=500",
        "name": "Vermeer Industries Peppermint Raspberry Candy"
      },
      "revenue": 3809712,
      "units": 6852
    }
  ],
  "sales_over_time_week": {
    "1": {
      "orders": 96,
      "total": 270240
    },
    "2": {
      "orders": 31,
      "total": 74121
    },
    "3": {
      "orders": 52,
      "total": 180284
    },
    "4": {
      "orders": 34,
      "total": 115600
    },
    "5": {
      "orders": 67,
      "total": 333325
    },
    "6": {
      "orders": 57,
      "total": 374262
    },
    "7": {
      "orders": 26,
      "total": 35672
    }
  },
  "sales_over_time_year": {
    "1": {
      "orders": 330,
      "total": 2952510
    },
    "10": {
      "orders": 746,
      "total": 2322298
    },
    "11": {
      "orders": 5424,
      "total": 16863216
    },
    "12": {
      "orders": 680,
      "total": 3198040
    },
    "2": {
      "orders": 745,
      "total": 7034290
    },
    "3": {
      "orders": 687,
      "total": 6486654
    },
    "4": {
      "orders": 311,
      "total": 1593253
    },
    "5": {
      "orders": 44,
      "total": 166452
    },
    "6": {
      "orders": 403,
      "total": 3514966
    },
    "7": {
      "orders": 342,
      "total": 1870398
    },
    "8": {
      "orders": 696,
      "total": 2628096
    },
    "9": {
      "orders": 279,
      "total": 1401138
    }
  }
}
```

When you make a request to the [dashboard endpoint](#retrieve-dashboard-information), you will receive the dashboard object in your response. This contains information on products and sales figures.

Attribute | Type | Description
----------|------|-------------
`bestsellers` | obect | Metadata on the 30 best selling products
`sales_over_time_week` | object | The total number of orders and units sold per week
`sales_over_time_year` | object | The total number of orders and units sold per month

## Retrieve dashboard information

```shell
curl https://freddy.codesubmit.io/dashboard \
-H "Authorization: Bearer {access_token}"
```

> You will receive the [dashboard object](#the-dashboard-object) in your response:

```json
{
  "dashboard": {
    "bestsellers": [
      {
        "product": {
          "id": "e2414f21-2647-c4aa-748a-81dc838db74a",
          "image": "https://images.unsplash.com/photo-1463860914822-61dc3ee606f7?crop=entropy&cs=tinysrgb&fit=crop&fm=jpg&h=500&ixid=eyJhcHBfaWQiOjF9&ixlib=rb-1.2.1&q=80&w=500",
          "name": "Cartoon Network Studios Lime Flower Youngberry Gummies"
        },
        "revenue": 2835702,
        "units": 6178
      }
    ],
    "sales_over_time_week": {
      "1": {
        "orders": 96,
        "total": 270240
      },
      "2": {
        "orders": 31,
        "total": 74121
      },
      "3": {
        "orders": 52,
        "total": 180284
      },
      "4": {
        "orders": 34,
        "total": 115600
      },
      "5": {
        "orders": 67,
        "total": 333325
      },
      "6": {
        "orders": 57,
        "total": 374262
      },
      "7": {
        "orders": 26,
        "total": 35672
      }
    },
    "sales_over_time_year": {
      "1": {
        "orders": 330,
        "total": 2952510
      },
      "10": {
        "orders": 746,
        "total": 2322298
      },
      "11": {
        "orders": 5424,
        "total": 16863216
      },
      "12": {
        "orders": 680,
        "total": 3198040
      },
      "2": {
        "orders": 745,
        "total": 7034290
      },
      "3": {
        "orders": 687,
        "total": 6486654
      },
      "4": {
        "orders": 311,
        "total": 1593253
      },
      "5": {
        "orders": 44,
        "total": 166452
      },
      "6": {
        "orders": 403,
        "total": 3514966
      },
      "7": {
        "orders": 342,
        "total": 1870398
      },
      "8": {
        "orders": 696,
        "total": 2628096
      },
      "9": {
        "orders": 279,
        "total": 1401138
      }
    }
  }
}
```

Access [the dashboard object](#the-dashboard-object) through this endpoint, which contains product metadata and sales figures.

### Endpoint

`GET https://freddy.codesubmit.io/dashboard`

# Orders

## The orders object

>

```json
{
  "created_at": "2019-10-14T21:26:48.915215",
  "currency": "$",
  "customer": {
    "address": {
      "city": "Angleton",
      "street": "Battery",
      "zipcode": "42194"
    },
    "avatar": "https://api.adorable.io/avatars/256/6772b722a64fc9875c2b1fc773ee5f34.png",
    "email": "glandarious2040@yandex.com",
    "id": "5c5cddec-98b3-f834-f34c-062f2886bcd4",
    "name": "Cyrus",
    "surname": "Hooper"
  },
  "id": "dd5fe07b-bcf3-96d3-7f38-843178c992a3",
  "product": {
    "id": "4511d7aa-36b8-e0d0-cfb4-a64ca8999390",
    "image": "https://images.unsplash.com/photo-1474625342403-1b8a2c0f7215?crop=entropy&cs=tinysrgb&fit=crop&fm=jpg&h=500&ixid=eyJhcHBfaWQiOjF9&ixlib=rb-1.2.1&q=80&w=500",
    "name": "Zig Zag Children Clothes Cilantro Lowbush Cranberry Drops",
    "quantity": 99
  },
  "status": "shipped",
  "total": 5230
}
```

When you make a request to the [orders endpoint](#retrieve-order-history), you will receive the orders object in the reponse. The orders objects contains information on past orders.

Attribute | Type | Description
----------|------|-------------
`created_at` | ISO 8601 date | Timestamp for when the order was placed
`currency` | string | Currency in which the order was placed
`customer` | object | Metadata on the customer that placed the order
`id`       | string | UUID for the ordered product
`product`  | object | Metadata on the ordered product
`status`   | string | Current order status (either `processing`, `shipped`, or `delivered`)
`total`    | integer| The total order amount in USD


## Retrieve order history

```shell
curl https://freddy.codesubmit.io/orders?q=glandarious2040 \
-H "Authorization: Bearer {access_token}"
```

> This request returns the [orders object](#the-orders-object):

```json
{
  "orders": [
    {
      "created_at": "2019-10-14T21:26:48.915215",
      "currency": "$",
      "customer": {
        "address": {
          "city": "Angleton",
          "street": "Battery",
          "zipcode": "42194"
        },
        "avatar": "https://api.adorable.io/avatars/256/6772b722a64fc9875c2b1fc773ee5f34.png",
        "email": "glandarious2040@yandex.com",
        "id": "5c5cddec-98b3-f834-f34c-062f2886bcd4",
        "name": "Cyrus",
        "surname": "Hooper"
      },
      "id": "dd5fe07b-bcf3-96d3-7f38-843178c992a3",
      "product": {
        "id": "4511d7aa-36b8-e0d0-cfb4-a64ca8999390",
        "image": "https://images.unsplash.com/photo-1474625342403-1b8a2c0f7215?crop=entropy&cs=tinysrgb&fit=crop&fm=jpg&h=500&ixid=eyJhcHBfaWQiOjF9&ixlib=rb-1.2.1&q=80&w=500",
        "name": "Zig Zag Children Clothes Cilantro Lowbush Cranberry Drops",
        "quantity": 99
      },
      "status": "shipped",
      "total": 5230
    }
  ],
  "page": 1,
  "total": 1
}
```

Access the [orders history object](#the-orders-history-object) through this endpoint, which contains information on past orders, such as product and customer metadata and current order status.

### Endpoint

`GET https://freddy.codesubmit.io/orders`

### Path parameters

Parameter | Description
--------- | -----------
`page` | Choose what page of the results you want in your response. The response provides 50 orders per page.
`q` | Search for a specific word or phrase within the order history