---
title: Badalaa Developer API Documentation

language_tabs: # must be one of https://git.io/vQNgJ
  - shell: cURL

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/lord/slate'>Powered by Slate</a>



search: true
---

# Introduction

> API Endpoint

```shell
http://api.badalaa.com/api/v1/
```

Welcome to the Badalaa API! The API is organized around [REST](https://en.wikipedia.org/wiki/Representational_state_transfer). Our API has predictable, resource-oriented URLs, and uses HTTP response codes to indicate API errors.

This API reference provides information on available endpoints and how to interact with it. 

We have language bindings in Shell (PHP and Python comimg soon!). You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.

## Making Requests

As per RESTful design patterns, Badalaa API implements following HTTP verbs:

* **`GET`** - Read resources
* **`POST`** - Create new resources
* **`PUT`** - Modify existing resources
* **`DELETE`** - Remove resources

`POST` requests must have a JSON encoded body and the `Content-Type: application/json` header.

## Errors

Badalaa uses standard HTTP response codes to indicate success or failure of an API request. In general, codes in the 2xx range indicate success, codes in the 4xx range indicate an error that resulted from the provided information (e.g., a required parameter was missing), and codes in the 5xx range indicate an error with Badalaa's servers.

Status Code | Meaning
---------- | -------
400 | Bad Request -- The request is missing key information or is malformed.
401 | Unauthorized -- Your API key is wrong.
403 | Forbidden -- The resource requested is hidden for administrators only.
404 | Not Found -- The specified resource could not be found.
405 | Method Not Allowed -- You tried to access a resource with an invalid method.
500 | Internal Server Error -- We had a problem with our server. Try again later.
503 | Service Unavailable -- We're temporarily offline for maintenance. Please try again later.

# Authentication

> To authorize, use this code:

```shell
# With shell, you can just pass the correct header with each request
curl "api_endpoint_here"
  -H "Authorization: Token BADALAA_API_TOKEN_KEY"
```


> Make sure to replace `BADALAA_API_TOKEN_KEY` with your API key.

Badalaa uses API keys to allow access to the API. You can register and manage your API keys in the [Dashboard](http://api.badalaa.com/accounts/signup/).

Badalaa expects for the API key to be included in all API requests to the server in a header that looks like the following:

`Authorization: Token BADALAA_API_TOKEN_KEY`

<aside class="notice">
You must replace <code>BADALAA_API_TOKEN_KEY</code> with your personal API key.
</aside>

Your API keys carry many privileges, so be sure to keep them secure! Do not share your secret API keys in publicly accessible areas such GitHub, client-side code, and so forth.

# Product Categories

## Retrieve a product category

```shell
curl http://api.badalaa.com/api/v1/product_categories/{id}/
  -H "Authorization: Token BADALAA_API_TOKEN_KEY"
```

> The above command returns JSON structured like this:

```json
{
    "id": 1,
    "code":101,
    "name":"ELECTRONICS",
    "description":"Phones, Laptops, Fridges"
}
```

This endpoint lets you retrieve a product category by ID.

### HTTP Request

`GET http://api.badalaa.com/api/v1/product_categories/{id}/`

## List all product categories

```shell
curl http://api.badalaa.com/api/v1/product_categories/
  -H "Authorization: Token BADALAA_API_TOKEN_KEY"
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": 1,
    "code":101,
    "name":"ELECTRONICS",
    "description":"Phones, Laptops, Fridges"
  },
  {
    "id": 2,
    "code":102,
    "name":"BEAUTY",
    "description":"Makeup, Fragrances, Body Care"
  }
]
```
This endpoint retrieves all product categories.

### HTTP Request

`GET http://api.badalaa.com/api/v1/product_categories/`

# Orders

`Order` objects are created to handle end customers' purchases. You can create, retrieve, as well as list all orders. Orders are identified by an ID.

## Create an order

```shell
curl http://api.badalaa.com/api/v1/purchase/
  -X POST
  -H "Content-Type: application/json"
  -H "Authorization: Token BADALAA_API_TOKEN_KEY"
  --data '{"first_name":"John", "last_name":"Doe", "email":"john@mail.com", "product_category_code":"101", "product_selling_price": 5000}'
```

Creates a new `Order` object. This is similar to making a purchase.

### HTTP Request

`POST http://api.badalaa.com/api/v1/purchase/`

### Arguments

Parameter | Description
--------- | -----------
first_name | First name of the customer placing the order.
last_name | Last name of the customer placing the order.
email | The email address of the customer placing the order.
product_category_code | Category code of the prouct being purchased. See [Product Categories](#product-categories).
product_selling_price | Total amount paid for the product.

