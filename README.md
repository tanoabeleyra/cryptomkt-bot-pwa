# CryptoMKT Bot
![icon](https://tanoabeleyra.github.io/cryptomkt-bot-webapp/static/icon-192.png)
> A web app for a trading bot running on [CryptoMarket](https://www.cryptomkt.com).

## Build Setup
``` bash
# install dependencies
npm install

# serve with hot reload at localhost:8080
npm run dev

# build for production with minification
npm run build
```

## About the API
The API must run on SSL (port 443) and allow [CORS](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing).

You can protect the API with [JWT](https://en.wikipedia.org/wiki/JSON_Web_Token).  
An `Authorization` header with the following format is sent with every request: `JWT <token>`

### Endpoints
`POST /auth`
> Obtain the JWT
- Payload
  ```
  {
    "username": [string],
    "password": [string]
  }
  ```
- Response
  ```
  {
    "access_token": [string]
  }
  ```
---
`GET /buyer/<market>`
> Get the buyer trading on market `<market>`
- Response
  ```
  {
    "remaining_amount": [number],
    "remaining_fiat": [number]
  }
  ```
---
`PATCH /buyer/<market>`
> Update the buyer trading on market `<market>`
- Payload
  ```
  {
    "remaining_amount": [number],
    "remianing_fiat": [number]
  }
  ```
- Response: Same as `GET /buyer/<market_code>`
---
`GET /seller/<market_code>`
> Get the seller trading on market `<market>`
- Response:
  ```
  {
    "remaining_fiat": [number],
    "min_spread": [number]
  }
  ```
---
`PATCH /seller/<market_code>`
> Update the seller trading on market `<market>`
- Payload
  ```
  {
    "remaining_fiat": [number],
    "min_spread": [number]
  }
  ```
- Response: Same as `GET /seller/<market_code>`
--- 
`GET /orders/<id>`
> Get the order with id `<id>`
- Response: data from `GET api.cryptomkt.com/v1/orders/status?id=<id>`
--- 
`POST /orders/<market>`
> Open an order on market `<market>`
- Payload
  ```
  {
    "amount": [number],
    "price: [number],
    "type": [string]
  }
  ```
  `type` is either *buy* or *sell*.

- Response: data from `POST api.cryptomkt.com/v1/orders/create`
---
`DELETE /orders/<id>`
> Cancel the order with id `<id>`
- Response: data from `POST api.cryptomkt.com/v1/orders/cancel?id=<id>`
---
`GET /orders/active/<market>`
> Get the active orders for market `<market>`
- Response: data from `GET api.cryptomkt.com/v1/orders/active?market=<market>`
---
`GET /orders/executed/<market>`
> Get the executed orders for market `<market>`
- Response: data from `GET api.cryptomkt.com/v1/orders/executed?market=<market>`
---
`GET /balance`
> Get your CryptoMarket balance
- Response: data from `GET api.cryptomkt.com/v1/balance`
