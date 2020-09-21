---
title: API Reference

language_tabs:
  - javascript

toc_footers:
  - <a href='https://digitexfutures.com/'>Go to Digitex Futures</a>
  - <a href='https://github.com/slatedocs/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true

code_clipboard: true
---

# Introduction

Welcome to Digitex Futures API!

You can use our API to get the market data and manage your orders on Digitex Futures Exchange.

Visit https://github.com/DigitexOfficial/api-docs to leave your feedback. Code example is located in `examples` folder. 

# REST API

## Overview

Please, use the following URLs to send requests.

**Testnet**: `https://rest.tapi.digitexfutures.com`.

**Mainnet**: `https://rest.mapi.digitexfutures.com`.

## Response format

Every response message is a JSON-object with the following fields.

Name | Type | Description
---- | ---- | -----------
status | string | valid values are `ok` and `error`
data | object or array | response payload
code | integer | optional; is set to an error code if `status` is `error`
msg | string | optional; human readable error description if `status` is `error` 

All timestamps are provided in milliseconds until other noted. 

> An example of a successfull response:

```javascript
{
  "status": "ok",
  "data": {}
}
```

> An example of an error response:

```javascript
{
  "status": "error",
  "code": 2222,
  "msg": "error description"
}
```

**Note:** the error will also be returned in case of system maintenance and absence of data for the response. 

## Public - Ping

Use it to test if Digitex Futures API is reachable.

**Request**

`GET /api/v1/public/ping`

**Parameters**

*This method takes no parameters*

**Response**

*The response object has no fields*

> An example of a response from 'public/ping':

```javascript
{}
```

## Public - Announcement

Get the latest public announcements.

**Request**

`GET /api/v1/public/announcement`

**Parameters**

*This method takes no parameters*

**Response**

Name | Type | Description
---- | ---- | -----------
id | integer | announcement's ID 
link | string | link to a full announcement
title | string | announcement's title
content | string | detailed description
date | string | date and time of the announcement
tags | list of strings | arbitrary set of tags
urgent | bool | whether this announcement is urgent or not

> An example of a response from 'public/announcement':

```javascript
{
  "status": "ok",
  "ts":1590402678700,
  "data": [
    {
      "id": 1,
      "link": "string",
      "title": "string",
      "content": "string",
      "date": "2020-05-21T08:08:49.464Z",
      "tags": ["tag1", "tag2"],
      "urgent": true,
    },
    {
      "id": 2,
      "link": "string",
      "title": "string",
      "content": "string",
      "date": "2020-05-21T08:08:49.464Z",
      "tags": ["tag3"],
      "urgent": false,
    }
  ]
}
```

## Public - Time

Get the current date and time.

**Request**

`GET /api/v1/public/time`

**Parameters**

*This method takes no parameters*

**Response**

Name | Type | Description
---- | ---- | -----------
iso | string | current UTC time (ISO 8601 with milliseconds)  
timestamp | integer | current UTC timestamp in milliseconds

> An example of a response from 'public/time':

```javascript
{
    "status":"ok",
    "data":{
        "iso":"2020-06-01T09:17:46.825",
        "timestamp":1590992266825
    }
}
```

## Public - Contracts

Get the list of contracts traded on Difitex Futures Exchange.

**Request**

`GET /api/v1/public/contracts`

**Parameters**

*This method takes no parameters*

**Response**

Name | Type | Description
---- | ---- | -----------
id | integer | contract's unique ID
name | string | contract's name
symbol | string | contract's unique symbol
type | string | type of the contract
isTradable | bool | if this contract is tradable
baseCurrency | string | base currency of the contract
quoteCurrency | string | quote currency of the contract
pnlCurrency | string | currency of the contract's PnL
marginCurrency | string | currency of the contract's margin
settleCurrency | string | contract's settlement currency
lotSize | integer | number of contracts per lot
isQuanto | bool | if contract is quanto
isInverse | bool | if contract is inverse
underlyingAsset | string | type of the underlying asset
indexSymbol | string | symbol of the contract's index
premiumIndexSymbol | string | symbol of the contract's premium index
fundingRate | float | funding rate value
fundingPeriod | integer | duration of the funding perion in seconds
indicativeFundingRate | float | indicative funding rate value
markType | string | type of the mark method
initMargin | float | initial margin value (in percents)
maintMargin | float | maintenance margin value (in percents)
deleverage | bool | if deleverage available for the contract
isLeverage | bool | if leverage can be used
maxLeverage | integer | maximum value of the leverage
createTime | integer | contract's creation timestamp
listingTime | integer | contract's listing timestamp
expiryTime | integer | contract's expiry timestamp
settleTime | integer | contract's settlement timestamp
makerFee | float | maker's fee value
takerFee | float | taker's fee value
settlementFee | float | settlement fee value
insuranceFee | float | insurance fee value
minPrice | float | minimum price of the contract
maxPrice | float | maximum price of the contract
minOrderSize | float | minimum order size
maxOrderSize | float | maximum order size
tickSize | float | contract's tick size in quoted currency
tickValue | float | contract's tick value in base currency

> An example of a response from 'public/contracts':

```javascript
{
    "status":"ok",
    "ts":1597073306274,
    "data":[
        {
            "id":1,
            "marketId":1,
            "name":"BTC/USD-PERP",
            "symbol":"BTCUSD-PERP",
            "type":"perpetual_futures",
            "isTradable":true,
            "baseCurrency":"BTC",
            "quoteCurrency":"USD",
            "pnlCurrency":"DGTX",
            "marginCurrency":"DGTX",
            "settleCurrency":"DGTX",
            "lotSize":1,
            "isQuanto":true,
            "isInverse":false,
            "underlyingAsset":"coin",
            "indexSymbol":".DGTXBTCUSD",
            "premiumIndexSymbol":"",
            "fundingRate":0.01,
            "fundingPeriod":28800,
            "indicativeFundingRate":0,
            "markType":"fair_price",
            "initMargin":1,
            "maintMargin":0.5,
            "deleverage":true,
            "isLeverage":true,
            "maxLeverage":25,
            "createTime":1588003200000,
            "listingTime":1588003200000,
            "expiryTime":0,
            "settleTime":0,
            "makerFee":0,
            "takerFee":0,
            "settlementFee":0,
            "insuranceFee":0,
            "minPrice":0,
            "maxPrice":0,
            "minOrderSize":0,
            "maxOrderSize":0,
            "tickSize":5,
            "tickValue":0.1
        },
        {
            "id":2,
            "marketId":2,
            "name":"ETH/USD-PERP",
            "symbol":"ETHUSD-PERP",
            "type":"perpetual_futures",
            "isTradable":true,
            "baseCurrency":"ETH",
            "quoteCurrency":"USD",
            "pnlCurrency":"DGTX",
            "marginCurrency":"DGTX",
            "settleCurrency":"DGTX",
            "lotSize":1,
            "isQuanto":true,
            "isInverse":false,
            "underlyingAsset":"coin",
            "indexSymbol":".DGTXETHUSD",
            "premiumIndexSymbol":"",
            "fundingRate":0.01,
            "fundingPeriod":28800,
            "indicativeFundingRate":0,
            "markType":"fair_price",
            "initMargin":1,
            "maintMargin":0.5,
            "deleverage":true,
            "isLeverage":true,
            "maxLeverage":25,
            "createTime":1588003200000,
            "listingTime":0,
            "expiryTime":0,
            "settleTime":0,
            "makerFee":0,
            "takerFee":0,
            "settlementFee":0,
            "insuranceFee":0,
            "minPrice":0,
            "maxPrice":0,
            "minOrderSize":0,
            "maxOrderSize":0,
            "tickSize":0.25,
            "tickValue":0.25,
            "priceIncrement":1
        }
    ]
}
```

## Public - Assets

**Request**

`GET /api/v1/public/assets`

**Parameters**

*This method takes no parameters*

**Response**

Name | Type | Description
---- | ---- | -----------
name | string | asset's name
symbol | string | asset's symbol
type | string | asset's type
precision | integer | asset's precision
hasDeposit | bool | if deposit of the asset is available
hasWithdraw | bool | if withdrawal of the asset is available
depositFee | float | deposit fee value
withdrawFee | float | withdrawal fee value
minDepositSize | float | minimum deposit size
maxDepositSize | float| minimum withdrawal size

> An example of a response from 'public/assets':

```javascript
{
   "status":"ok",
   "ts":1590428686166,
   "data":[
       {
         "id":1,
         "name":"Digitex Token",
         "symbol":"DGTX",
         "type":"token",
         "precision":4,
         "hasDeposit":true,
         "hasWithdraw":true,
         "depositFee":0,
         "withdrawFee":0,
         "minDepositSize":0,
         "maxDepositSize":0
      },
      {
         "id":2,
         "name":"Bitcoin",
         "symbol":"BTC",
         "type":"coin",
         "precision":8,
         "hasDeposit":false,
         "hasWithdraw":false,
         "depositFee":0,
         "withdrawFee":0,
         "minDepositSize":0,
         "maxDepositSize":0
      },
      {
         "id":3,
         "name":"US Dollar",
         "symbol":"USD",
         "type":"coin",
         "precision":2,
         "hasDeposit":false,
         "hasWithdraw":false,
         "depositFee":0,
         "withdrawFee":0,
         "minDepositSize":0,
         "maxDepositSize":0
      },
      {
         "id":4,
         "name":"Ethereum",
         "symbol":"ETH",
         "type":"coin",
         "precision":8,
         "hasDeposit":false,
         "hasWithdraw":false,
         "depositFee":0,
         "withdrawFee":0,
         "minDepositSize":0,
         "maxDepositSize":0
      },
      {
         "id":5,
         "name":"Ripple",
         "symbol":"XRP",
         "type":"coin",
         "precision":8,
         "hasDeposit":false,
         "hasWithdraw":false,
         "depositFee":0,
         "withdrawFee":0,
         "minDepositSize":0,
         "maxDepositSize":0
      }
   ]
}
```

## Public - Orderbook

Get the current orderbook snapshot.

**Request**

`GET /api/v1/public/orderbook`

**Parameters**

Name | Type | Description
---- | ---- | -----------
symbol | string | contract's symbol
depth | integer | desired orderbook depth; default: 5, max: 200

**Response**

Name | Type | Description
---- | ---- | -----------
symbol | string | contract's symbol
updated | integer | timestamp of the update
bids | list of pairs [price, amount] | orderbook bids
asks | list of pairs [price, amount] | orderbook asks

> An example of a response from 'public/orderbook':

```javascript
{
    "status":"ok",
    "ts":1590737035730,
    "data":{
        "symbol":"BTCUSD-PERP",
        "updated":1590737035653,
        "bids":[
            [9530,15432],
            [9525,12640],
            [9520,73561],
            [9515,68109],
            [9510,19895]
        ],
        "asks":[
            [9535,63584],
            [9540,51424],
            [9545,79901],
            [9550,56939],
            [9555,161822]
        ]
    }
}
```

## Public - Markets

Get the overview of a current state of all available markets and 24-hour stats.

**Request**

`GET /api/v1/public/markets`

**Parameters**

*This method takes no parameters*

**Response**

Name | Type | Description
---- | ---- | -----------
symbol | string | contract's symbol
openTime | integer | start timestamp of a 24h-interval
closeTime | integer | end timestamp of the interval
openPx | float | price value at the beginning of the interval
highPx | float | the highest price during the interval
lowPx | float | the lowest price during the interval
pxChange24h | float | price change during the interval
volume24h | float | total trade volume (in contracts) during the interval
volume24hUsd | float | total trade volume (in USD) during the interval
fundingTime | integer | next funding time
fundingRate | float | current funding rate
bestBidPx | float | current best bid price
bestBidQty | float | current best bid quatity
bestAskPx | float | current best ask price
bestAskQty | float | current best ask quantity
lastTradePx | float | last trade price
lastTradeQty | float | last trade quantity
lastTradeTs | integer | last trade timestamp
contractValue | float | contract value in DGTX
openInterest | float | open interest value in contracts
openInterestUsd | float | open interest value in USD
dgtxUsdRate | float | current DGTX/USD rate
insuranceFund | float | insurance fund value

> An example of a response from 'public/markets':

```javascript
{
    "status":"ok",
    "ts":1590993332256,
    "data":[
        {
            "symbol":"BTCUSD-PERP",
            "openTime":1590906900000,
            "closeTime":1590993300000,
            "openPx": 9450,
            "highPx24h":9640,
            "lowPx24h":9390,
            "pxChange24h": -3.35,
            "volume24h":682494894,
            "volume24hUsd":2852425063.05,
            "fundingTime":1590998400000,
            "fundingRate":0.0003,
            "bestBidPx":9555,
            "bestBidQty":16424,
            "bestAskPx":9560,
            "bestAskQty":31076,
            "lastTradePx":9555,
            "lastTradeQty":4936,
            "lastTradeTs":1590993332183,
            "contractValue":194.9,
            "openInterest":431229,
            "openInterestUsd":4586283.33,
            "dgtxUsdRate":0.03728994,
            "insuranceFund":1711653380.28
        },
        {
            "symbol":"ETHUSD-PERP",
            "openTime":1599558120000,
            "closeTime":1599644520000,
            "openPx":342.75,
            "highPx24h":346.5,
            "lowPx24h":325.5,
            "pxChange24h":0.66,
            "volume24h":983328,
            "volume24hUsd":11797492.97,
            "fundingTime":1599667200000,
            "fundingRate":0.01,
            "bestBidPx":344.75,
            "bestBidQty":88,
            "bestAskPx":345,
            "bestAskQty":573,
            "lastTradePx":345,
            "lastTradeQty":186,
            "lastTradeTs":1599644494456,
            "contractValue":345,
            "openInterest":9465,
            "openInterestUsd":116110.45,
            "dgtxUsdRate":0.03555753,
            "insuranceFund":239178.5,
            "markPx":346.7181
        }
    ]
}
```

## Public - Trades

Get the latest contract's trades.

**Request**

`GET /api/v1/public/trades`

**Parameters**

Name | Type | Description
---- | ---- | -----------
symbol | string | contract's symbol
count | integer | desired number of trades; default: 100, max: 200

**Response**

Name | Type | Description
---- | ---- | -----------
symbol | string | contract's symbol
ts | integer | trade timestamp 
px | float | trade price
qty | float | trade quantity
side | string |  trade side

> An example of a response from 'public/trades':

```javascript
{
    "status":"ok",
    "ts":1590737141606,
    "data":{
        "symbol":"BTCUSD-PERP",
        "trades":[
            {"ts":1593783145314,"px":9110,"qty":276,"side":"SELL"},
            {"ts":1593783145314,"px":9110,"qty":1,"side":"SELL"},
            {"ts":1593783145317,"px":9110,"qty":157,"side":"SELL"},
            {"ts":1593783145319,"px":9110,"qty":1,"side":"SELL"},
            {"ts":1593783145323,"px":9110,"qty":24,"side":"SELL"}
        ]
    }
}
```

## Public - Klines

Get the latest K-lines of the contract.

**Request**

`GET /api/v1/public/klines`

**Parameters**

Name | Type | Description
---- | ---- | -----------
symbol | string | contract's symbol
count | integer | desired number of klines; default: 60, max: 1500
interval | string | kline's interval; default: 1min;
from | integer | start timestamp of the interval
to | integer | end timestamp of the interval

*Note*: currently only interval `1min` is supported. Fields `from` and `to` are not supported yet.

**Response**

Name | Type | Description
---- | ---- | -----------
symbol | string | contract's symbol
interval | string | kline's interval
id | integer | kline's ID
o | float | open price
h | float | highest price
l | float | lowest price
c | float | close price
v | float | total volume

> An example of a response from 'public/klines':

```javascript
{
    "status":"ok",
    "ts":1590737272724,
    "data":{
        "symbol":"BTCUSD-PERP",
        "interval": "1min",
        "klines":[
            {
                "id":1590736620,
                "o":9535,
                "h":9545,
                "l":9530,
                "c":9540,
                "v":382175
            },
            {
                "id":1590736680,
                "o":9540,
                "h":9545,
                "l":9525,
                "c":9530,
                "v":474006
            }
        ]
    }
}
```

## Public - Index

Get contract's index current value.

**Request**

`GET /api/v1/public/index`

**Parameters**

Name | Type | Description
---- | ---- | -----------
symbol | string | symbol of the index

*Note*: if `symbol` is not specified the list of all indices will be returned.

**Response**

Name | Type | Description
---- | ---- | -----------
indexSymbol | string | symbol of the index (e.g. `.DGTXBTCUSD`)
contracts | list of strings | list of contracts that have this index as underlying index
updated | integer | latest update timestamp
markPx | float | current mark price value
fairPx | float | current fair price value
spotPx | float | current spot price value
components | list of objects | components of the index
weight | float | weight of the particular component in final price
ts | integer | timestamp of the last update
px | float | last trade value
vol | float | last trade volume

> An example of a response from 'public/index':

```javascript
{
    "status":"ok",
    "ts":1590999736854,
    "data":{
        ".DGTXBTCUSD":{
            "indexSymbol":".DGTXBTCUSD",
            "contracts":["BTCUSD-PERP"],
            "updated":1590999736783,
            "markPx":9549.44,
            "fairPx":9549.44,
            "spotPx":9549.44,
            "components":{
                "binance":{
                    "weight":25,"ts":0,"px":0,"vol":0
                },
                "bitfinex":{
                    "weight":25,"ts":0,"px":0,"vol":0
                },
                "coinbasepro":{
                    "weight":25,"ts":0,"px":0,"vol":0
                },
                "kraken":{
                    "weight":25,"ts":0,"px":0,"vol":0
                }
            }
        }
    }
}
```

## Public - Liquidations

Get latest liquidations of the contract.

**Request**

`GET /api/v1/public/liquidations`

**Parameters**

Name | Type | Description
---- | ---- | -----------
symbol | string | contract's symbol

**Response**

Name | Type | Description
---- | ---- | -----------
symbol | string | contract's symbol
positions | list of objects | list of liquidated positions
ts | integer | liquidation timestamp
qty | float | liquidated position quantity
px | float | liquidated position price
type | string | liquidated position type (`LONG` or `SHORT`)

> An example of a response from 'public/liquidations':

```javascript
{
    "status":"ok",
    "ts":1593780179450,
    "data":{
        "symbol":"BTCUSD-PERP",
        "positions":[
            {
                "ts":1593780350000,
                "qty":100,
                "px":9100,
                "type":"LONG"
            }
        ]
    }
}
```

# Websockets API

## Overview

Use the following URLs to connect to Digitex Futures websockets API:

*Testnet*: `wss://ws.tapi.digitexfutures.com`.

*Mainnet*: `wss://ws.mapi.digitexfutures.com`.

Server send message `ping` every 30 seconds. Client should respond with message `pong` or it would be disconnected. 

## Message format

**Request**

Each request is a JSON-object with the following structure:

Name | Type | Description
---- | ---- | -----------
id | integer | request ID
method | string | request method name
params | list of strings | request method parameters 

The field `id` is used in JSON as an identifier of the request. The response for the particular request has the same `id` value.

**Response**

Every response is a JSON-object with the following fields:

Name | Type | Description
---- | ---- | -----------
status | string | valid values are `ok` and `error`
result | object or array | response payload
code | integer | optional; is set to an error code if `status` is `error`
msg | string | optional; human readable error description if `status` is `error` 

> An example of a successfull response:

```javascript
{
    "id": 1,
    "status": "ok"
}
```

> An example of an error response:

```javascript
{
    "id": 1,
    "status": "error",
    "code": 3003,
    "msg": "contract not found"
}
```

## Public channels

Channel name has the following format: `BTCUSD-PERP@orderbook_25`.

Full list of public channels:

- orderbook_*depth*; possible *depth* values: `1`, `5`, `10`, `25`, `50` of `full`.

- kline_*interval*, possible *interval* values: `1min`, `3min`, `5min`, `15min`, `30min`, `1h`, `3h`, `6h`, `12h`, `1D`, `3D`, `1W`, `3W`, `1M`, `3M`, `6M`, `1Y`.

- trades.

- liquidations.

- ticker.

- fundingInfo.

- index.

## Public - Subscribe

Subscribe for a particular channel.

**Request**

Field | Value
----- | -----
method | `subscribe`
params | one or more channels

> An example of the subscribe request:

```javascript
{
    "id": 1,
    "method": "subscribe",
    "params": [
        "BTCUSD-PERP@orderbook_25"
    ]
}
```

## Public - Unsubscribe

Unsubscribe from a particular channel.

**Request**

Field | Value
----- | -----
method | `unsubscribe`
params | one or more channels

> An example of the unsubscribe request:

```javascript
{
    "id": 1,
    "method": "unsubscribe",
    "params": [
        "BTCUSD-PERP@orderbook_25"
    ]
}
```

## Public - Subscription list

Get the list of active subscriptions.

**Request**

Field | Value
----- | ----- 
method | `subscriptions`
params | empty; can be omitted

**Response**

Name | Type | Description
---- | ---- | -----------
id | integer | request's ID
status | string | indicates success or failure
result | array of strings | list of trader's active subscriptions

> An example of a response with subscription list:

```javascript
{
    "id":2,
    "status":"ok",
    "result":[
        "BTCUSD-PERP@orderbook_5",
        "BTCUSD-PERP@kline_1min"
    ]
} 
```

## Published messages

Each published by the exchange message is a JSON-object with the following fields:

Name | Type | Description
---- | ---- | -----------
ch | string | full channel name (e.g. `BTCUSD-PERP@trades`)
data | object | channel-specific payload

## Public - Orderbook channel

Realtime stream of contract's orderbook.

**Channel name:** `<symbol>@orderbook_X` (put allowed depth instead of `X`).

Possible values of orderbook depth have been described earlier.

**Message**

The payload has the following fields:

Name | Type | Description
---- | ---- | -----------
symbol | string | contract's symbol
ts | integer | last update timestamp
bids | list of pairs [price, quantity] | current bids
asks | list of pairs [price, quantity] | current asks

> An example of an `orderbook` message:

```javascript
{
    "ch":"orderbook_5",
    "data":{
        "symbol":"BTCUSD-PERP",
        "ts":1591295037813,
        "bids":[
            [9840,53914],[9835,26103],[9830,37644],[9825,21331],[9820,43942]
        ],
        "asks":[
            [9845,15899],[9850,85810],[9855,41480],[9860,39565],[9865,40374]
        ]
    }
} 
```

## Public - Trades channel

Realtime stream of contract's trades.

**Channel name:** `<symbol>@trades`.

**Message**

The payload has the following fields:

Name | Type | Description
---- | ---- | -----------
symbol | string | contract's symbol
trades | array of objects | list of trades
ts | integer | trade's timestamp
px | float | trade's price
qty | float | trade's quantity

> An example of a `trades` message:

```javascript
{
    "ch":"trades",
    "data":{
        "symbol":"BTCUSD-PERP",
        "trades":[
            {"px":9845,"qty":2356,"ts":1591295123213},
            {"px":9845,"qty":75,"ts":1591295123213}
        ]
    }
} 
```

## Public - Kline channel

Realtime stream of contract's candles. Klines are published every minute.

**Channel name:** `<symbol>@kline_1min`

Currently only `1min` interval is supported.

**Message**

Name | Type | Description
---- | ---- | -----------
symbol | string | contract's symbol
interval | string | kline's interval
id | integer | kline's ID
o | float | open price
h | float | highest price
l | float | lowest price
c | float | close price
v | float | total trade volume

> An example of a `kline` message:

```javascript
{
    "ch":"kline_1min",
    "data":{
        "symbol":"BTCUSD-PERP",
        "interval":"1min",
        "id":1591295280,
        "o":9835,
        "h":9840,
        "l":9825,
        "c":9830,
        "v":654088
    }
}
```

## Public - Liquidations channel

Realtime stream of liquidated positions of the contract.

**Channel name:** `<symbol>@liquidations`.

**Message**

Name | Type | Description
---- | ---- | -----------
symbol | string | contract's symbol
positions | array of objects | list of liquidated positions
ts | integer | liquidation's timestamp
qty | float | liquidated position size
px | float | liquidation price
type | string | liquidated position type (`LONG` or `SHORT`)

> An example of a `liquidations` message:

```javascript
{
    "ch":"liquidations",
    "data":{
        "symbol":"BTCUSD-PERP",
        "positions":[
            {"ts":1594039337113,"qty":75,"px":9255,"type":"SHORT"}
        ]
    }
}
```

## Public - Ticker channel

Realtime updates of contract's stats.

**Channel name:** `<symbol>@ticker`.

**Message**

Name | Type | Description
---- | ---- | -----------
symbol | string | contract's symbol
openTime | integer | start timestamp of a 24h-interval
closeTime | integer | end timestamp of the interval
openPx | float | price value at the beginning of the interval
highPx | float | the highest price during the interval
lowPx | float | the lowest price during the interval
pxChange24h | float | price change during the interval
volume24h | float | total trade volume (in contracts) during the interval
volume24hUsd | float | total trade volume (in USD) during the interval
bidPx | float | current best bid price
bidQty | float | current best bid quatity
askPx | float | current best ask price
askQty | float | current best ask quantity
lastPx | float | last trade price
lastQty | float | last trade quantity
fundingRate | float | current funding rate
fundingTime | integer | next funding time
contractValue | float | contract value in DGTX
openInterest | float | open interest value in contracts
openInterestUsd | float | open interest value in USD
dgtxUsdRate | float | current DGTX/USD rate
insuranceFund | float | insurance fund value

`openInterestUsd` is calculated as: `openInterest` * `contractValue` * `dgtxUsdRate`.

`contractValue` is calculated as: `lastTradePx` / `TICK_SIZE` * `TICK_VALUE`, where:

- `TICK_SIZE`=5 and `TICK_VALUE`=0.1 for `BTCUSD-PERP` contract;
- `TICK_SIZE`=0.25 and `TICK_VALUE`=0.25 for `ETHUSD-PERP` contract.
- `TICK_SIZE`=1 and `TICK_VALUE`=0.1 for `XRPUSD-PERP` contract.

> An example of `ticker` message:

```javascript
{
    "ch":"ticker",
    "data":{
        "symbol":"BTCUSD-PERP",
        "openTime":1590906900000,
        "closeTime":1590993300000,
        "openPx": 9250,
        "highPx24h":9450,
        "lowPx24h":9100,
        "pxChange24h": -3.35,
        "volume24h":78053288,
        "volume24hUsd":2852425063.05,
        "bidPx":9420,
        "bidQty":100,
        "askPx":9450,
        "askQty":250,
        "lastPx":9400,
        "lastQty":200,
        "fundingRate":0.0003,
        "nextFundingTime":123456789000,
        "contractValue":194.9,
        "openInterest":431229,
        "openInterestUsd":4586283.33,
        "dgtxUsdRate":0.03728994,
        "insuranceFund": 1711659412.9
    }
}
```

## Public - Funding Info channel

Realtime stream of contract's funding information.

**Channel name:** `<symbol>@fundingInfo`.

**Message**

Name | Type | Description
---- | ---- | -----------
symbol | string | contract's symbol
ts | integer | funding info update timestamp
rate | float | current funding rate value

> An example of `fundingInfo` message:

```javascript
{
    "ch":"fundingInfo",
    "data":{
        "symbol":"BTCUSD-PERP",
        "ts":157743360000,
        "rate":0.0003
    }
}
```

## Public - Index channel

Realtime stream of contract's index price.

**Channel name:** `<symbol>@index`.

Symbol can be either a contract symbol (`BTCUSD-PERP`) or index symbol (`.DGTXBTCUSD`).

**Message**

Name | Type | Description
---- | ---- | -----------
indexSymbol | string | contract's symbol
ts | integer | timestamp of the last update
markPx | float | current mark price value
fairPx | float | current fair price value
spotPx | float | current spot price value
components | list of objects | components of the index
weight | float | weight of the particular component in final price
ts | component's price updated timestamp
px | float | last trade value
vol | float | last trade volume

> An example of `index` message:

```javascript
{
    "ch":"index",
    "data":{
        "indexSymbol":".DGTXBTCUSD",
        "ts":1590999736783,
        "markPx":9549,
        "fairPx":9549,
        "spotPx":9565,
        "components":{
            "binance":{"weight":25,"ts":0,"px":0,"vol":0},
            "bitfinex":{"weight":25,"ts":0,"px":0,"vol":0},
            "coinbasepro":{"weight":25,"ts":0,"px":0,"vol":0},
            "kraken":{"weight":25,"ts":0,"px":0,"vol":0}
        }
    }
}
```

## Public - Errors

In case of a general error the `error` message will be sent by the server.

> An example of an `error` message:

```javascript
{
    "ch":"error",
    "data":{
        "code":1,
        "msg":"error description"
    }
}
```

## Private - Trading

Private methods of the API allow to manage orders and position.

To obtain an API key for your account, you need to be logged in exchange, then open Account and go to **API** tab. Then click "Create" to generate your private API key.

**General**

Possible values of order's `status`:  `PENDING`, `ACCEPTED`, `REJECTED`, `CANCELLED`, `FILLED`, `PARTIALLY_FILLED`, `TERMINATED`, `EXPIRED`, `TRIGGERED`.

Possible values of `ordType`: `MARKET`, `LIMIT`.

Possible values of `timeInForce`: `GFD` (Good-For-Day), `GTC` (Good-Till-Cancel), `GTF` (Good-Till-Funding), `IOC` (Immediate-Or-Cancel), `FOK` (Fill-Or-Kill).

Possible values of `side`: `BUY`, `SELL`.

Possible values of `ch` (channel name): `error`, `orderStatus`, `orderFilled`, `orderCancelled`, `contractClosed`, `traderStatus`, `traderBalance`, `position`, `funding`, `leverage`, `condOrderStatus`.

Trader don't need to subscribe for trading messages. They will be sent by the server after successfull authentication. 

For `BTCUSD-PERP`: order price should be positive and a <u>multiple of 5</u>, order quantity should be positive and <u>integral</u>.

For `ETHUSD-PERP`: order price should be positive and a <u>multiple of 0.25</u>, order quantity should be positive and <u>integral</u>.

For `XRPUSD-PERP`: order price should be positive and a <u>multiple of 1</u>, order quantity should be positive and <u>integral</u>.

All timestamps are provided in milliseconds.

<u>Note</u>: the trader cannot have a mix of long and short contracts in his/her position.

**Rate limit**

Currently our trading API allows up to 10 requests per second.

**Order chain**

Each active order in the engine has a unique order identifier (`clOrdId`). 

Value of the `clOrdId` is assigned by the trader. It should be a unique string for each order. This string can be any length, but only the first 16 bytes are used by the exchange. If the length is less than 16 bytes the trading engine will add zero bytes to make it 16 bytes total.

This original order identifier is preserved in `origClOrdId` field of the order-related messages.

Orders are immutable objects in the engine, that means that any modification to the order (full or partial fill, quantity change or leverage change, cancellation) creates a **new** order with `clOrdId` generated bu the engine. The new identifier is reported to the trader in `newClOrdId` field, and the previous (old) order identifier is reported in `oldClOrdId` field.

Full fill or cancellation also create a new empty order with a quantity 0.

Therefore the full life cycle of an order is represented by a chain of orders. All orders in the chain have the same `origClOrdId` equal to the `clOrdId` of the `placeOrder` message. The last order in the chain has `qty` field equal to 0, and all orders in the chain except the first have `oldClOrdId` field referring to the previous order in the chain.

**Contract chain**

Contracts (or position) represent future contracts in possession of a trader. 

Each contract has a unique identifier (`contractId`) and the trader can close a particular contract using this identifier.

Contracts are immutable and any change to the existing contract, including its closing, liquidation or settlement results in creation of a **new** contract. 

Life cycle of a contract is represented by a contract chain. The last contract in the chain has `qty` equal to 0.
All contracts in the chain except the first one have `oldContractId` field referring to the previous contract in the chain.
All contracts in the chain have `origContractId` field equal to `contractId` of the first contract in the chain.
Field `oldClOrdId` is the identifier of the order that was matched and resulted in the first contract in the contract chain.

If neither fields `isIncrease`, `isFunding`, `isLiquidation` are set, the contract is created from another contract by increasing/decreasing (possibly to 0) the quantity of that contract.

A terminal contract is a contract with `qty` equal to 0. The terminal contract is always the last contract in a contract chain.
A terminal contract is created when a contract is fully closed by matching an order on the opposite side, or in case of liquidation.

## Private - Authentication

To start sending orders thrader should authenticate.

**Request**

Name | Value
---- | ----- 
method | should be "auth"
params | request parameters
type | should be "token"
value | set your API key

> An example of an `auth` request:

```javascript
{
    "id":2,
    "method":"auth",
    "params":{
        "type":"token",
        "value":"b78b6a9529b6a1161abcef24df2b36b82ee12f5c"
    }
}
```

**Response**

The server will respond with an appropriate `status` value.

If provided token isn't valid trader will receive an error response.

Trader needs to send again the `auth` message with the token every time he/she gets this error.

> An example of the failed auth response:

```javascript
{
    "id":2,
    "status":"error",
    "code":10501,
    "msg":"invalid credentials"
}
```

## Private - Trading status

If authentication was successful and trading engine is ready to receive and process trader's requests the following message will be received:

Name | Value
---- | ----- 
ch | "tradingStatus"
data | payload object
available | true or false

> An example of a trader status message:

```javascript
{
    "ch":"tradingStatus",
    "data":{
        "available":true
    }
}
```

This message indicates that trader can start trading.

In case of maintenance, connection issues, etc. trader will receive this message with field `available` set to `false`.

This message indicates that trading is not available in that very moment.

> An example of a trading status message if trading is not allowed:

```javascript
{
    "ch":"tradingStatus",
    "data":{
        "available":false
    }
}
```

## Private - Place order

**Request**

Name | Type | Description
---- | ---- | -----------
id | integer | request's ID
method | string | should be `placeOrder`
params | object | request parameters
symbol | string | contract's symbol
clOrdId | string | client-provided order's ID; optional
ordType | string | order's type
timeInForce | string | order's time-in-force
side | string | order's side
px | float | order's price; optional
qty | float | order's quantity

In case of `MARKET` order field `px` could be omitted.

`clOrdId` could be omitted. In this case it will be auto-generated by the server.

> An example of a `placeOrder` message:

```javascript
{
    "id":3,
    "method":"placeOrder",
    "params":{
        "symbol":"BTCUSD-PERP",
        "clOrdId":"c61533a0113c416b",
        "ordType":"MARKET",
        "timeInForce":"IOC",
        "side":"BUY",
        "px":0,
        "qty":10
    }
}
```

**Response**

The order can be either accepted or rejected by the exchange.

> An example of the `orderStatus` message if order has been accepted:

```javascript
{
    "ch":"orderStatus",
    "data":{
        "symbol":"BTCUSD-PERP",
        "timestamp":1597736006705,
        "clOrdId":"c61533a0113c416b",
        "origClOrdId":"c61533a0113c416b",
        "orderStatus":"ACCEPTED",
        "openTime":1597736006705,
        "orderType":"MARKET",
        "timeInForce":"IOC",
        "orderSide":"BUY",
        "qty":10,
        "px":0,
        "paidPx":2450,
        "leverage":5,
        "traderBalance":104705.4583,
        "orderMargin":0,
        "positionMargin":490,
        "upnl":0,
        "pnl":-5.2492,
        "markPx":12242.9113,
        "origQty":10
    }
}
```

The value of `clOrdId` can be used to cancel this order in the future (in case of `LIMIT` order).

`orderStatus` will have a value `ACCEPTED` or `REJECTED`. In case of `REJECTED` order a field `errCode` is set to appropriate error code.

`leverage` contains current trader's leverage.

`openTime` is the timestamp when the original `placeOrder` has been handled by the trading engine.

`origQty` is the quantity of the original order.

`paidPx` is the amount of funds locked on the trader's account as the margin. If `leverage` is 1, `paidPx` equals to `px`. 

`traderBalance` is the current trading balance of the trader.

`orderMargin` is the amount of funds locked in all active orders. 

`positionMargin` is the total amount of funds locked in the position (contracts, active orders). 

`upnl` is the unrealized PnL at this moment.

`pnl` is the realized PnL, i.e. the change to the trader balance achieved as the result of all trading operations since the last funding. Explicit trader's transfers to/from trading account are not accounted into PnL.

## Private - Order fills

When order is filled trader will receive the message with the fill's details.

`status` contains the order fill status. It is either `FILLED` if the order has been filled entirely, or `PARTIALLY_FILLED` if the order has been partially filled.

If the order has been partially filled, either the remainder of the order stays in the orderbook as a **new** order, or the remainder of the order is cancelled.

If the remainder of the order is cancelled, field `droppedQty` contains the quantity of the cancelled part of the order. 

In case of partial fill either `qty` > 0  or `droppedQty` > 0 but not both.

If the order has been entirely filled `qty` == 0 and `droppedQty` == 0.

`positionType` is `LONG` if the trader has long position, `SHORT` if the trader has short position.

`positionContracts` is the total amount of contracts held by the trader. This value is always non-negative. `positionVolume` is the total monetary value of the position. It is computed as sum of `px` * `qty` over all active contracts.

`positionLiquidationVolume` is the total monetary value of all liquidations of the position, i.e. sum of `liquidationPx` * `qty` over all active contracts.

`positionBankruptcyVolume` is the same for the bankruptcy price.

`contracts` contains a list of contacts that were changed as the result of this fill. 

`entryPx` is the entry price of the contract.

`paidPx` is the price which is held as position margin per unit.

`exitPx` holds the price at which the quantity was decreased.

`entryQty` contains total quantity of all increases to the contract chain.

`exitQty` contains total quantity of all decreases to the contract chain.

As opposed to the increases, the decreases may be at different exit prices, so field `exitVolume` contains the volume of all exits to the contract chain.

`fundingCount` contains number of fundings performed during the lifetime of this contract chain.

`fundingPaidPx` is the accumulated value of fundings per one unit in terms of the market price.

`fundingQty` is the total number of units accumulated during all fundings.

`fundingVolume` is the total volume (`px` * `qty`) of all funding during the contract lifetime.

<u>Note</u>: the funding information is reset to 0 if the quantity of the contract is increased and the trader has enough funds on his/her trading balance to replenish the position margin for this contract to the original value.

Trader can use the value of `contractId` to close specific contract in the future using this ID.

`openTime` is the timestamp of the first contract in the contract chain.

`marketTrades` contains the list of trades of this trader performed as the result of the fill.

`isMaker` is set to 1, if this trade resulted from filling up the order already in the orderbook.

<u>Note</u>: the value of `newClOrdId` is generated by the exchange (16 bytes). It's the ID of `FILLED` order and this order has the reference to the originally placed order via `origClOrdId`.


> An example of the `orderFilled` message:

```javascript
{
    "ch":"orderFilled",
    "data":{
        "symbol":"BTCUSD-PERP",
        "timestamp":1597736006705,
        "newClOrdId":"genrated-by-the-engine",
        "clOrdId":"c61533a0113c416b",
        "origClOrdId":"c61533a0113c416b",
        "openTime":1597736006705,
        "orderStatus":"FILLED",
        "orderType":"MARKET",
        "timeInForce":"IOC",
        "orderSide":"BUY",
        "qty":0,
        "origQty":10,
        "droppedQty":0,
        "px":0,
        "paidPx":0,
        "leverage":5,
        "traderBalance":104705.4583,
        "orderMargin":0,
        "positionMargin":490,
        "upnl":0,
        "pnl":-5.2492,
        "positionContracts":10,
        "positionVolume":122500,
        "positionLiquidationVolume":110250,
        "positionBankruptcyVolume":98000,
        "positionType":"LONG",
        "markPx":12242.9113,
        "contracts":[
            {
                "timestamp":1597736006705,
                "contractId":678850017,
                "traderId":94889,
                "positionType":"LONG",
                "qty":10,
                "entryPx":12250,
                "leverage":5,
                "paidPx":2450,
                "entryQty":10,
                "exitPx":0,
                "exitQty":0,
                "exitVolume":0,
                "liquidationPx":11025,
                "bankruptcyPx":9800,
                "isIncrease":1,
                "fundingPaidPx":0,
                "fundingQty":0,
                "fundingVolume":0,
                "fundingCount":0,
                "oldClOrdId":"c61533a0113c416b",
                "openTime":1597736006705,
                "origContractId":678850017
            }
        ],
        "marketTrades":[
            {
                "side":"BUY",
                "px":12250,
                "paidPx":2450,
                "qty":10,
                "leverage":5,
                "isMaker":0
            }
        ]
    }
}
```

## Private - Cancel order

Specific order can be cancelled using its `clOrdId`.

**Request**

Name | Type | Description
---- | ---- | -----------
id | integer | request's ID
method | string | should be "cancelOrder"
params | object | request's parameters
symbol | string | contract's symbol
clOrdId | string | client-provided or assigned by the API

> An example of single order cancellation:

```javascript
{
    "id":4,
    "method":"cancelOrder",
    "params":{
        "symbol":"BTCUSD-PERP",
        "clOrdId":"fbad327328cf46f7"
    }
} 
```

More than one order can be cancelled as well.

Trader can cancel all the orders (`side` and `px` are omitted) or just orders with the specified `side`  and/or `px`.

> An example of multiple order cancellation:

```javascript
{
    "id":5,
    "method":"cancelAllOrders",
    "params":{
        "symbol":"BTCUSD-PERP",
        "px":0,
        "side":"BUY"
    }
}
```

**Response**

The `orderCancelled` will be received as a result of order cancellation.

<u>Note</u>: `CANCELLED` order ID (`clOrdId`) - differs from ID of a placed order (`oldClOrdId`).

Another valid values for `orderStatus` are `TERMINATED` and `EXPIRED` which are used when orders are cancelled by the exchange.

In case of error `orderStatus` will be set to `REJECTED` and `errCode` will indicate the error.

`GFD` (good-for-day) orders are cancelled automatically by the engine at 00:00:00 UTC of the next day. The trader will receive `orderCancelled`with the `orderStatus` equals to `EXPIRED`.

`GTF` (good-till-funding) orders are cancelled automatically by the engine at the next funding (i.e 00:00:00, 08:00:00, 16:00:00 UTC). The trader will receive `orderCancelled` with the `orderStatus` equals to `EXPIRED`.

Field `orders` contains all the orders that have been cancelled. 

<u>Note</u>: the value of `clOrdId` is generated by the exchange (16 bytes).

> An example of `orderCancelled` message:

```javascript
{
    "ch":"orderCancelled",
    "data":{
        "symbol":"BTCUSD-PERP",
        "timestamp":1597737437444,
        "orderStatus":"CANCELLED",
        "orders":[
            {
                "clOrdId":"genrated-by-the-engine",
                "timestamp":1597737427442,
                "traderId":94889,
                "orderType":"LIMIT",
                "timeInForce":"GTC",
                "orderSide":"BUY",
                "px":11425,
                "qty":25,
                "leverage":5,
                "paidPx":2285,
                "origQty":25,
                "oldClOrdId":"4835b0cf874d49a3",
                "origClOrdId":"4835b0cf874d49a3",
                "openTime":1597737427442
            },
            {
                "clOrdId":"genrated-by-the-engine",
                "timestamp":1597737427440,
                "traderId":94889,
                "orderType":"LIMIT",
                "orderSide":"BUY",
                "timeInForce":"GTC",
                "px":11450,
                "qty":15,
                "leverage":5,
                "paidPx":2290,
                "origQty":15,
                "oldClOrdId":"039c7e730ccd4f5d",
                "origClOrdId":"039c7e730ccd4f5d",
                "openTime":1597737427440
            }
        ],
        "traderBalance":104705.4583,
        "orderMargin":0,
        "positionMargin":980,
        "upnl":0,
        "pnl":-5.2492,
        "markPx":12249.1363
    }
}
```

## Private - Place conditional order

Trader can schedule order placement if particular condition would be met. The value of either `SPOT_PRICE` or `LAST_PRICE` can act as a trigger.

**Request**

Name | Type | Description
---- | ---- | -----------
id | integer | request's ID
method | string | should be "placeCondOrder"
params | object | request's parameters
symbol | string | contract's symbol
actionId | string | conditional action's ID; optional
pxType | string | triggered price type
condition | string | triggered condition
pxValue | float | triggered value
clOrdId | string | client-provided order's ID; optional
ordType | string | order's type
timeInForce | string | order's time-in-force
side | string | order's side
px | float | order's price; optional
qty | float | order's quantity
mayIncrPosition | bool | if order is allowed to increase trader's position

`actionId` can be set by the trader or will be generated by the exchange. This value can be used later to cancel conditional order placement.

`pxType` can be either `SPOT_PRICE` or `LAST_PRICE`.

<u>Note</u>: currently only `SPOT_PRICE` is supported.

`condition` represents the condition that should be met. Possible values: `GREATER_EQUAL`, `LESS_EQUAL`.

`pxValue` is the value to which `SPOT_PRICE` or `LAST_PRICE` will be compared using `condition`.

`mayIncrPosition` should be set to `true` if the order is allowed to change the sign of the trader's position.

When the condition is triggered a new order with the parameters `symbol`, `clOrdId`, `ordType`, `timeInForce`, `side`, `px`, `qty` will be placed. 

> An example of a `placeCondOrder` request:

```javascript
{
    "id":4,
    "method":"placeCondOrder",
    "params":{
        "symbol":"BTCUSD-PERP",
        "actionId":"a5b90ca768754b75",
        "pxType":"SPOT_PRICE",
        "condition":"LESS_EQUAL",
        "pxValue":9105,
        "clOrdId":"010e2b91e5214410",
        "ordType":"LIMIT",
        "timeInForce":"GTC",
        "side":"BUY",
        "px":9105,
        "qty":100,
        "mayIncrPosition": true
    }
} 
```

**Response**

If a conditional order was created successfully the exchange will send the `condOrderStatus` message in response.

In case of an error the value of `status` will be set to `REJECTED` and `errCode` will provide the appropriate error code.

> An example of a `condOrderStatus` message:

```javascript
{
    "ch":"condOrderStatus",
    "data":{
        "symbol":"BTCUSD-PERP",
        "status":"ACCEPTED",
        "conditionalOrders":[
            {
                "ts":1594379135077,
                "actionId":"a5b90ca768754b75",
                "pxType":"SPOT_PRICE",
                "condition":"LESS_EQUAL",
                "pxValue":9105,
                "clOrdId":"010e2b91e5214410",
                "ordType":"LIMIT",
                "side":"BUY",
                "timeInForce":"GTC",
                "px":9105,
                "qty":100,
                "mayIncrPosition": true
            }
        ]
    }
}
```

When conditional order is triggered the exchange will inform the trader with the `condOrderStatus` message and activate the order. The value of field `status` will be set to `TRIGGERED`.

<u>Note</u>: the value of `actionId` is generated by the exchange (16 bytes).

> An example of a conditional order activation:

```javascript
{
    "ch":"condOrderStatus",
    "data":{
        "symbol":"BTCUSD-PERP",
        "status":"TRIGGERED",
        "conditionalOrders":[
            {
                "ts":1594383515908,
                "actionId":"generated-by-the-engine",
                "oldActionId":"0559991a2f042d6",
                "pxType":"SPOT_PRICE",
                "condition":"GREATER_EQUAL",
                "pxValue":9185,
                "clOrdId":"5689b870f57e4edf",
                "ordType":"MARKET",
                "side":"SELL",
                "timeInForce":"FOK",
                "px":0,
                "qty":25,
                "mayIncrPosition": true
            }
        ]
    }
} 
```

## Private - Cancel conditional order

The trader can cancel previously placed conditional order using corresponding `actionId`.

All conditional orders can be cancelled by setting `allForTrader` to `true`. In this case `actionId` can be omitted.

**Request**

Name | Type | Description
---- | ---- | -----------
id | integer | request's ID
method | string | should be "cancelCondOrder"
params | object | request's parameters
symbol | string | contract's symbol
actionId | string | conditional action's ID; optional
allForTrader | bool | if need to cancel all conditional orders

> An example of a `cancelCondOrder` request:

```javascript
{
    "id":4,
    "method":"cancelCondOrder",
    "params":{
        "symbol":"BTCUSD-PERP",
        "actionId":"a5b90ca768754b75",
        "allForTrader":false
    }
}
```

**Response**

For each cancelled conditional order the engine will generate a new `actionId`. 

The previous one will be assigned to a field `oldActionId`.

In case of an error the value of `status` will be set to `REJECTED` and `errCode` will contain the appropriate error code.

> An example of a response to conditional order cancellation:

```javascript
{
    "ch":"condOrderStatus",
    "data":{
        "symbol":"BTCUSD-PERP",
        "status":"CANCELLED",
        "conditionalOrders":[
            {
                "ts":1594379135077,
                "actionId":"generated-by-the-engine",
                "oldActionId":"a5b90ca768754b75",
                "pxType":"SPOT_PRICE",
                "condition":"LESS_EQUAL",
                "pxValue":9105,
                "clOrdId":"010e2b91e5214410",
                "ordType":"LIMIT",
                "side":"BUY",
                "timeInForce":"GTC",
                "px":9105,
                "qty":100,
                "mayIncrPosition": true
            }
        ]
    }
}
```

## Private - Close contract

Trader can close a specific contract using its ID (`contractId`). 

There is an option to specify order type (`MARKET` or `LIMIT`), price (only for `LIMIT`) and quantity (to close only a part of the contract) for a contract close operation.

**Request**

Name | Type | Description
---- | ---- | -----------
id | integer | request's ID
method | string | should be "closeContract"
params | object | request's parameters
symbol | string | contract's symbol
contractId | integer | contract's ID
ordType | string | order's type
px | float | order's price; required for `LIMIT` order only
qty | float | order's quantity; optional

> An example of a `closeContract` request:

```javascript
{
    "id":3,
    "method":"closeContract",
    "params":{
        "symbol":"BTCUSD-PERP",
        "contractId":678871417,
        "ordType":"MARKET",
        "px":0,
        "qty":30
    }
}
```

**Response**

`orderIds` contains an array of `clOrdId`s which have been created by the exchange to close the contract.

If an error occurs (e.g. unknown `contractId`) an array `orderIds` will be empty and `errCode` will be set to appropriate value.

> An example of a `contractClosed` message:

```javascript
{
    "ch":"contractClosed",
    "data":{
        "symbol":"BTCUSD-PERP",
        "orderIds":[
            "generated-by-the-engine"
        ]
    }
} 
```

<u>Note</u>: if the trader closes only a part of the contract the exchange will generate **new** ID for the remained part of the contract (this ID can be found in `orderFilled` message).

Trader also will receive `orderStatus` and `orderFilled` messages related to these orders. The latter one will contain the information about affected contracts.

> An example of `orderStatus` message followed by the `contractClosed`:

```javascript
{
    "ch":"orderStatus",
    "data":{
        "symbol":"BTCUSD-PERP",
        "timestamp":1597739258241,
        "openTime":1597739258241,
        "orderStatus":"ACCEPTED",
        "orderType":"MARKET",
        "timeInForce":"GTC",
        "orderSide":"SELL",
        "px":0,
        "paidPx":0,
        "qty":20,
        "traderBalance":104712.9683,
        "orderMargin":0,
        "positionMargin":0,
        "upnl":0,
        "pnl":7.51,
        "markPx":12269.9768,
        "leverage":5,
        "oldContractId":678871417,
        "clOrdId":"generated-by-the-engine",
        "origClOrdId":"generated-by-the-engine",
        "origQty":20
    }
}
```

> An example of `orderFilled` message followed by the `contractClosed` and `orderStatus`:

```javascript
{
    "ch":"orderFilled",
    "data":{
        "symbol":"BTCUSD-PERP",
        "timestamp":1597739258241,
        "clOrdId":"generated-by-the-engine",
        "newClOrdId":"generated-by-the-engine",
        "origClOrdId":"generated-by-the-engine",
        "openTime":1597739258241,
        "orderStatus":"FILLED",
        "orderType":"MARKET",
        "orderSide":"SELL",
        "timeInForce":"GTC",
        "px":0,
        "leverage":5,
        "paidPx":0,
        "qty":0,
        "origQty":20,
        "droppedQty":0,
        "traderBalance":104712.9683,
        "orderMargin":0,
        "positionMargin":0,
        "upnl":0,
        "pnl":7.51,
        "positionContracts":0,
        "positionVolume":0,
        "positionLiquidationVolume":0,
        "positionBankruptcyVolume":0,
        "markPx":12269.9768,
        "contracts":[
            {
                "timestamp":1597737600000,
                "traderId":94889,
                "contractId":678896018,
                "origContractId":678850017,
                "oldContractId":678871417,
                "openTime":1597736006705,
                "positionType":"LONG",
                "qty":0,
                "entryPx":12250,
                "entryQty":20,
                "exitPx":12270,
                "exitQty":20,
                "exitVolume":245400,
                "leverage":5,
                "paidPx":2450,
                "liquidationPx":11030,
                "bankruptcyPx":9801.225,
                "fundingPaidPx":1.225,
                "fundingQty":20,
                "fundingVolume":24.5,
                "fundingCount":1
            }
        ],
        "marketTrades":[
            {
                "px":12270,
                "paidPx":2454,
                "qty":20,
                "leverage":5,
                "isMaker":0
            }
        ]
    }
}
```

## Private - Close position

The trader can close the position (all available contracts) via `closePosition` request.

**Request**

Name | Type | Description
---- | ---- | -----------
id | integer | request's ID
method | string | should be "closePosition"
params | object | request's parameters
symbol | string | contract's symbol
ordType | string | closing order's type
px | float | closing order's price; required for `LIMIT` order only

Trader can specify `ordType` (`MARKET` or `LIMIT`) and `px` (if `ordType` is set to `LIMIT`).

A sequence of messages that will be received as a result is the same as in the case of closing a single contract (`contractClosed`, `orderStatus`, `orderFilled`).

> An example of a `closePosition` request:

```javascript
{
    "id":8,
    "method":"closePosition",
    "params":{
        "symbol":"BTCUSD-PERP",
        "ordType":"MARKET",
        "px":0
    }
}
```

## Private - Trader status request

Trader can request his/her status via the `getTraderStatus` message.

**Request**

Name | Type | Description
---- | ---- | -----------
id | integer | request's ID
method | string | should be "getTraderStatus"
params | object | request's parameters
symbol | string | contract's symbol

> An example of a `getTraderStatus` request:

```javascript
{
    "id":9,
    "method":"getTraderStatus",
    "params":{
        "symbol":"BTCUSD-PERP"
    }
}
```

**Response**

This message contains trader's balance, current position, active orders (can be cancelled using corresponding `clOrdId`), conditional orders (can be cancelled using corresponding `actionId`) and contracts (can be closed using corresponding `contractId`).

> An example of a `traderStatus` message:

```javascript
{
    "ch":"traderStatus",
    "data":{
        "symbol":"BTCUSD-PERP",
        "traderBalance":104712.9683,
        "leverage":5,
        "orderMargin":3360,
        "positionMargin":1226,
        "upnl":-5,
        "pnl":7.51,
        "markPx":12248.1077,
        "positionType":"LONG",
        "positionContracts":25,
        "positionVolume":306500,
        "positionLiquidationVolume":275875,
        "positionBankruptcyVolume":245200,
        "contracts":[
            {
                "timestamp":1597741150122,
                "traderId":94889,
                "positionType":"LONG",
                "qty":25,
                "entryPx":12260,
                "paidPx":2452,
                "liquidationPx":11035,
                "bankruptcyPx":9808,
                "exitPx":0,
                "leverage":5,
                "contractId":678924872,
                "openTime":1597741150122,
                "entryQty":25,
                "exitQty":0,
                "exitVolume":0,
                "fundingPaidPx":0,
                "fundingQty":0,
                "fundingVolume":0,
                "fundingCount":0,
                "origContractId":678924872
            }
        ],
        "activeOrders":[
            {
                "clOrdId":"00e5cd4c246e43d3",
                "timestamp":1597741243498,
                "openTime":1597741243498,
                "orderType":"LIMIT",
                "timeInForce":"GTF",
                "orderSide":"BUY",
                "px":12000,
                "qty":70,
                "leverage":5,
                "paidPx":2400,
                "origClOrdId":"00e5cd4c246e43d3",
                "origQty":70
            }
        ],
        "conditionalOrders":[
            {
                "ts":1597741315769,
                "actionId":"KJuA1w0H59grJPjD",
                "pxType":"SPOT_PRICE",
                "condition":"LESS_EQUAL",
                "pxValue":12000,
                "clOrdId":"1597741315728445",
                "ordType":"MARKET",
                "side":"BUY",
                "timeInForce":"IOC",
                "px":0,
                "qty":30,
                "mayIncrPosition":true
            }
        ]
    }
}
```

## Private - Change leverage

Trader can change the value of current leverage via `changeLeverageAll` request.

**Request**

Name | Type | Description
---- | ---- | -----------
id | integer | request's ID
method | string | should be "changeLeverageAll"
params | object | request's parameters
symbol | string | contract's symbol
leverage | integer | new leverage value

> An example of a `changeLeverageAll` request:

```javascript
{
    "id":2,
    "method":"changeLeverageAll",
    "params":{
        "symbol":"BTCUSD-PERP",
        "leverage":10
    }
}
```

**Response**

This message contains trader's balance, current position, active orders (can be cancelled using corresponding `clOrdId`) and contracts (can be closed using corresponding `contractId`) according to a new leverage value.

<u>Note</u>: trader must renew contracts and active orders on his/her side according to the new values of `contracts` and `activeOrders`.  After this operation (leverage changing) all trader's contracts and active orders will change their identifiers - trading engine will assign the new ones to them.

In case of error (e.g. invalid new leverage value) the response will contain the appropriate `errCode` and `contracts`, `activeOrders` will be empty. Nothing will change.

> An example of a `leverage` message:

```javascript
{
    "ch":"leverage",
    "data":{
        "symbol":"BTCUSD-PERP",
        "leverage":10,
        "traderBalance":104712.9683,
        "orderMargin":1680,
        "positionMargin":613,
        "upnl":-12.5,
        "pnl":7.51,
        "positionType":"LONG",
        "positionContracts":25,
        "positionVolume":306500,
        "positionLiquidationVolume":291250,
        "positionBankruptcyVolume":275850,
        "contracts":[
            {
                "timestamp":1597741932768,
                "contractId":678935965,
                "oldContractId":678924872,
                "openTime":1597741150122,
                "traderId":94889,
                "positionType":"LONG",
                "qty":25,
                "entryPx":12260,
                "paidPx":1226,
                "entryQty":25,
                "exitPx":0,
                "exitQty":0,
                "exitVolume":0,
                "leverage":10,
                "liquidationPx":11650,
                "bankruptcyPx":11034,
                "fundingPaidPx":0,
                "fundingQty":0,
                "fundingVolume":0,
                "fundingCount":0,
                "origContractId":678924872
            }
        ],
        "activeOrders":[
            {
                "clOrdId":"generated-by-engine",
                "timestamp":1597741243498,
                "traderId":94889,
                "orderType":"LIMIT",
                "timeInForce":"GTF",
                "orderSide":"BUY",
                "px":12000,
                "qty":70,
                "paidPx":1200,
                "leverage":10,
                "oldClOrdId":"00e5cd4c246e43d3",
                "origClOrdId":"00e5cd4c246e43d3",
                "openTime":1597741243498,
                "origQty":70
            }
        ]
    }
}
```

## Private - Funding

Trader will receive the `funding` message if he/she has open position during funding.

**Message**

`payoutPerContract` is the value of the payout per contract during the funding.

> An example of a `funding` message:

```javascript
{
    "ch":"funding",
    "data":{
        "symbol":"BTCUSD-PERP",
        "traderBalance":100549.736,
        "orderMargin":0,
        "positionMargin":1850.59,
        "upnl":0,
        "pnl":0,
        "positionContracts":0,
        "positionVolume":0,
        "positionLiquidationVolume":0,
        "positionBankruptcyVolume":0,
        "payout":-1.86,
        "payoutPerContract":0.0186,
        "markPx":238.8477,
        "positionMarginChange":-1.86,
        "contracts":[
            {
                "timestamp":1594137600000,
                "traderId":94889,
                "contractId":614339945,
                "oldContractId":614224561,
                "openTime":1594122555760,
                "positionType":"LONG",
                "qty":25,
                "entryPx":9275,
                "paidPx":927.5,
                "entryQty":25,
                "liquidationPx":8815,
                "bankruptcyPx":8348.43,
                "exitPx":0,
                "exitQty":0,
                "exitVolume":0,
                "leverage":10,
                "fundingPaidPx":0.93,
                "fundingQty":25,
                "fundingVolume":23.25,
                "fundingCount":1,
                "isFunding":1,
                "origContractId":614053631
            },
            {
                ...omitted...
            },
            {
                ...omitted...
            }
        ]
    }
} 
```

## Private - Position

If trader's position has been liquidated and/or active orders have been terminated by the exchange the `position` message will be sent by the exchange.

**Message**

`liquidatedContracts` contains an array of liquidated contracts (the same structure as in `traderStatus` message). 

`oldContractId` represents the ID of liquidated contract.

`terminatedOrders` contains an array of `clOrdId`s of terminated orders.

> An example of a `position` message:

```javascript
{
    "ch":"position",
    "data":{
        "symbol":"BTCUSD-PERP",
        "liquidatedContracts":[
            {
                "contractId":680407585,
                "oldContractId":679984688,
                "isLiquidation":1,
                "entryPx":0,
                "paidPx":0,
                "liquidationPx":0,
                "bankruptcyPx":0,
                "qty":0,
                "exitPx":0,
                "entryQty":0,
                "exitQty":0,
                "exitVolume":0,
                "fundingPaidPx":0,
                "fundingQty":0,
                "fundingVolume":0,
                "fundingCount":0,
                "origContractId":679035345
            }
        ],
        "terminatedOrders":[],
        "traderBalanceIncrement":-612.055,
        "traderBalance":104049.3477,
        "positionType":"LONG",
        "positionContracts":27,
        "positionMargin":660.6994,
        "orderMargin":0,
        "upnl":-326.2,
        "pnl":-662.33,
        "positionVolume":330995,
        "positionLiquidationVolume":314530,
        "positionBankruptcyVolume":297960.03,
        "markPx":11654.9973
    }
}
```
