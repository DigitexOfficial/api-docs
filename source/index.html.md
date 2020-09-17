---
title: API Reference

language_tabs:
  - javascript

toc_footers:
  - <a href='https://github.com/slatedocs/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true

code_clipboard: true
---

# Introduction

Welcome to the Digitex Futures API!

You can use our API to get the market data and manage your orders on Digitex Futures Exchange.

All timestamps are provided in milliseconds until other noted. 

# REST API

## Overview

Please, use the following URLs to send requests.

**Testnet**: `https://rest.tapi.digitexfutures.com`.

**Mainnet**: `https://rest.mapi.digitexfutures.com`.

## Message format

Every response message is a JSON-object with the following fields.

Name | Type | Description
---- | ---- | -----------
status | string | valid values are `ok` and `error`
data | object or array | result data
code | integer | optional, is set to an error code if `status` is `error`
msg | string | optional, human readable error description if `status` is `error` 

> Example of a successfull response:

```javascript
{
  "status": "ok",
  "data": {}
}
```

> Example of an error response:

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

**Paramaters**

*This method takes no parameters*

**Response**

*The response object has no fields*

> Example of a response to 'public/ping':

```javascript
{}
```

## Public - Anoouncement

Get the latest public announcements.

**Request**

`GET /api/v1/public/announcement`

**Paramaters**

*This method takes no parameters*

**Response**

Name | Type | Description
---- | ---- | -----------
id | integer | announcement's ID 
link | string | link to a full announcement
title | string | announcement's title
content | string | detailed description
date | string | date and time of the announcement
tags | list of strings | arbitrary set of string tags
urgent | bool | whether this announcement is urgent or not

> Example of a response to 'public/announcement':

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

**Paramaters**

*This method takes no parameters*

**Response**

Name | Type | Description
---- | ---- | -----------
iso | string | current UTC time formatted with ISO 8601 with milliseconds  
timestamp | integer | current UTC timestamp with milliseconds

> Example of a response to 'public/time':

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

**Paramaters**

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
insuranceFee | float | isurance fee value
minPrice | float | minimum price of the contract
maxPrice | float | maximum price of the contract
minOrderSize | float | minimum order size
maxOrderSize | float | maximum order size
tickSize | float | contract's tick size in quoted currency
tickValue | float | contract's tick value in base currency

> Example of a response to 'public/contracts':

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

**Paramaters**

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

> Example of a response to 'public/assets'

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

**Paramaters**

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

> Example of a response to 'public/orderbook':

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

**Paramaters**

*This method takes no parameters*

**Response**

Name | Type | Description
---- | ---- | -----------
symbol | string | contract's symbol
openTime | integer | start timestamp of 24h-intervel
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

> Example of a response to 'public/markets':

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

Get the latest contract trades.

**Request**

`GET /api/v1/public/trades`

**Paramaters**

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

> Example of a response to 'public/trades':

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

**Paramaters**

Name | Type | Description
---- | ---- | -----------
symbol | string | contract's symbol
count | integer | desired number of klines; default: 60, max: 1500
interval | string | kline interval; default: 1min;
from | integer | start timestamp of the interval
to | integer | end timestamp of the interval

*Note*: currently only interval `1min` is supported. Fields `from` and `to` are not supported yet.

**Response**

Name | Type | Description
---- | ---- | -----------
symbol | string | contract's symbol
interval | string | kline interval
id | integer | kline ID
o | float | open price
h | float | highest price
l | float | lowest price
c | float | close price
v | float | total volume

> Example of a response to 'public/klines':

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

**Paramaters**

Name | Type | Description
---- | ---- | -----------
symbol | string | symbol of the index

*Note*: if `symbol` is not specified the list of all indices will be returned.

**Response**

Name | Type | Description
---- | ---- | -----------
indexSymbol | string | symbol of the index (e.g. `.DGTXBTCUSD`)
contracts | list of strings | list of contracts that hava this index as underlying index
updated | integer | latest update timestamp
markPx | float | current mark price value
fairPx | float | current fair price value
spotPx | float | current spot price value
components | list of objects | components of the index
weight | float | weight of the particular component in final price
ts | integer | timestamp of the last update
px | float | last trade value
vol | float | last trade volume

> Example of a response to 'public/index':

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
            "spotPx":0,
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

**Paramaters**

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

> Example of a response to 'public/liquidations':

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

# Websocket API

## Overview

Use the following URLs to connect to Digitex Futures websocket API:

*Testnet*: `wss://ws.tapi.digitexfutures.com`.

*Mainnet*: `wss://ws.mapi.digitexfutures.com`.

Server send message `ping` every 30 seconds. Client should respond with message `pong` or it would be disconnected. 

## Message format

Each request is a JSON-object with the following structure:

Name | Type | Description
---- | ---- | -----------
id | integer | request ID
method | string | request method name
params | list of strings | request method parameters 

The field `id` is used in JSON as an identifier of the request. The response for the particular request has the same `id` value.

Every response is a JSON-object with the following fields:

Name | Type | Description
---- | ---- | -----------
status | string | valid values are `ok` and `error`
result | object or array | result data
code | integer | optional, is set to an error code if `status` is `error`
msg | string | optional, human readable error description if `status` is `error` 

> Example of a successfull response:

```javascript
{
    "id": 1,
    "status": "ok"
}
```

> Example of an error response:

```javascript
{
    "id": 1,
    "status": "error",
    "code": 3003,
    "msg": "contract not found"
}
```

## Public channels

Channel name looks as the following: `BTCUSD-PERP@orderbook_25`.

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
----- | ----- |
method | `subscribe`
params | one or more channels

> Example of the subscription request:

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
----- | ----- |
method | `unsubscribe`
params | one or more channels

> Example of the subscription request:

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
----- | ----- |
method | `subscriptions`
params | empty; can be omitted

> Example of the subscription request:

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

Each published message is a JSON-object with the following fields:

Name | Type | Description
---- | ---- | -----------
ch | string | full channel name
data | object | channel-specific payload

## Public - Orderbook channel

Realtime stream of contract's orderbook.

**Channel name:** `<symbol>@orderbook_X` (put allowed depth instead of X).

Possible values of orderbook depth have been described earlier.

**Message**

The payload has the following fields:

Name | Type | Description
---- | ---- | -----------
symbol | string | contract's symbol
ts | integer | last update timestamp
bids | list of pairs [price, quantity] | current bids
asks | list of pairs [price, quantity] | current asks

> Example of orderbook message:

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
ts | integer | trade's timestamp
px | float | trade's price
qty | float | trade's quantity

> Example of trades message:

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

Realtime stream of contract's candles.
Klines are published every minute.

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

> Example of kline message:

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
ts | integer | liquidation's timestamp
qty | float | liquidated position size
px | float | liquidation price
type | string | liquidated position type (`LONG` or `SHORT`)

> Example of liquidations message:

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
openTime | integer | start timestamp of 24h-intervel
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

> Example of ticker message:

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

> Example of fundingInfo message:

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

> Example of index message:

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

## Private - Trading

**General**

Possible value of order's `status`:  `PENDING`, `ACCEPTED`, `REJECTED`, `CANCELLED`, `FILLED`, `PARTIALLY_FILLED`, `TERMINATED`, `EXPIRED`, `TRIGGERED`.

Possible values of `ordType`: `MARKET`, `LIMIT`.

Possible values of `timeInForce`: `GFD` (Good-For-Day), `GTC` (Good-Till-Cancel), `GTF` (Good-Till-Funding), `IOC` (Immediate-Or-Cancel), `FOK` (Fill-Or-Kill).

Possible values of `side`: `BUY`, `SELL`.

Possible values of `ch` (channel name): `error`, `orderStatus`, `orderFilled`, `orderCancelled`, `contractClosed`, `traderStatus`, `traderBalance`, `position`, `funding`, `leverage`, `condOrderStatus`.

Trader don't need to subscribe for trading messages. They will be sent by the server after successfull authentication. 

For `BTCUSD-PERP`: order price should be positive and a <u>multiple of 5</u>, order quantity should be positive and <u>integral</u>.

For `ETHUSD-PERP`: order price should be positive and a <u>multiple of 0.25</u>, order quantity should be positive and <u>integral</u>.

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

**Request**

Name | Value
---- | ----- 
method | "auth"
params | object with the following fields
type | "token"
value | set your API key

> Example of auth request:

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

> Example of the failed auth response:

```javascript
{
    "id":2,
    "status":"error",
    "code":10501,
    "msg":"invalid credentials"
}
```