---
title: Badalaa Developer API Documentation

language_tabs: # must be one of https://git.io/vQNgJ
  - shell: cURL
  - php: PHP
  - python: Python

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/lord/slate'>Powered by Slate</a>



search: true
---

# Introduction

> API Endpoint

```php
http://api.badalaa.com/api/v1/
```

```python
http://api.badalaa.com/api/v1/
```

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

```php
require 'kittn'

api = Kittn::APIClient.authorize!('BADALAA_API_TOKEN_KEY')
```

```python
import kittn

api = kittn.authorize('BADALAA_API_TOKEN_KEY')
```

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

```php
require 'kittn'

api = Kittn::APIClient.authorize!('BADALAA_API_TOKEN_KEY')
```

```python
import kittn

api = kittn.authorize('BADALAA_API_TOKEN_KEY')
```

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

```php
require 'kittn'

api = Kittn::APIClient.authorize!('BADALAA_API_TOKEN_KEY')
```

```python
import kittn

api = kittn.authorize('BADALAA_API_TOKEN_KEY')
```

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

## Get All Kittens

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('BADALAA_API_TOKEN_KEY')
api.kittens.get
```

```python
import kittn

api = kittn.authorize('BADALAA_API_TOKEN_KEY')
api.kittens.get()
```

```shell
curl "http://example.com/api/kittens"
  -H "Authorization: Token BADALAA_API_TOKEN_KEY"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('BADALAA_API_TOKEN_KEY');
let kittens = api.kittens.get();
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": 1,
    "name": "Fluffums",
    "breed": "calico",
    "fluffiness": 6,
    "cuteness": 7
  },
  {
    "id": 2,
    "name": "Max",
    "breed": "unknown",
    "fluffiness": 5,
    "cuteness": 10
  }
]
```

This endpoint retrieves all kittens.

### HTTP Request

`GET http://example.com/api/kittens`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
include_cats | false | If set to true, the result will also include cats.
available | true | If set to false, the result will include kittens that have already been adopted.

<aside class="success">
Remember — a happy kitten is an authenticated kitten!
</aside>

## Get a Specific Kitten

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('BADALAA_API_TOKEN_KEY')
api.kittens.get(2)
```

```python
import kittn

api = kittn.authorize('BADALAA_API_TOKEN_KEY')
api.kittens.get(2)
```

```shell
curl "http://example.com/api/kittens/2"
  -H "Authorization: BADALAA_API_TOKEN_KEY"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('BADALAA_API_TOKEN_KEY');
let max = api.kittens.get(2);
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "name": "Max",
  "breed": "unknown",
  "fluffiness": 5,
  "cuteness": 10
}
```

This endpoint retrieves a specific kitten.

<aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside>

### HTTP Request

`GET http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to retrieve

## Delete a Specific Kitten

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('BADALAA_API_TOKEN_KEY')
api.kittens.delete(2)
```

```python
import kittn

api = kittn.authorize('BADALAA_API_TOKEN_KEY')
api.kittens.delete(2)
```

```shell
curl "http://example.com/api/kittens/2"
  -X DELETE
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let max = api.kittens.delete(2);
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "deleted" : ":("
}
```

This endpoint deletes a specific kitten.

### HTTP Request

`DELETE http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to delete

