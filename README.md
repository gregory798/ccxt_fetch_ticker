# Problem :
When using CCXT, particularly "exchange.fetch_ticker(...)", some exchanges return "None" at "previousClose".

# Solution : (Python3)

Few lines of code to get the list of exchanges that returns the "previousClose" attribute when using "exchange.fetch_ticker(...)"

```python3
import ccxt

has_previous_close = set()

exchange_ids = ccxt.exchanges
for id in exchange_ids:
    try:
        exchange = getattr (ccxt, id) ()
        markets = exchange.load_markets()
        for m in markets:
            tick = exchange.fetch_ticker(m)
            previousClose = tick["previousClose"]
            if previousClose:
                has_previous_close.add(id)
            break
    except Exception as e:
        continue

print("These exchanges return the 'previousClose' attribute :")
print(has_previous_close)
```

So we (currently) get :


```python3
{'coinone', 'mexc3', 'currencycom', 'upbit', 'binance', 'binanceus'}
```
---
---
---

# Problem :
When using CCXT, particularly "exchange.fetch_ticker(...)", some exchanges return "None" at "open" and/or "high" and/or "low" and/or "close".

# Solution : (Python3)

Few lines of code to get the list of exchanges that returns the "open" and "high" and "low" and "close" attributes when using "exchange.fetch_ticker(...)"

```python3
import ccxt

has_all_ohlc = set()

exchange_ids = ccxt.exchanges
for id in exchange_ids:
    try:
        exchange = getattr (ccxt, id) ()
        markets = exchange.load_markets()
        for m in markets:
            tick = exchange.fetch_ticker(m)
            if tick["open"] and tick["high"] and tick["low"] and tick["close"]:
                has_all_ohlc.add(id)
            break
    except Exception as e:
        continue

print("These exchanges return the all OHLC attributes :")
print(has_all_ohlc)
```

So we (currently) get :


```python3
{'flowbtc', 'okex', 'mexc3', 'currencycom', 'bitvavo', 'wavesexchange', 'bigone', 'novadax', 'okx', 'fmfwio', 'hollaex', 'kucoin', 'coinone', 'wazirx', 'upbit', 'coinex', 'binanceusdm', 'btctradeua', 'zb', 'bequant', 'bitmart', 'bitcoincom', 'binancecoinm', 'binance', 'probit', 'bitstamp1', 'okex5', 'mexc', 'bitbns', 'bitfinex2', 'bithumb', 'bybit', 'hitbtc', 'bitpanda', 'hitbtc3', 'ndax', 'btcturk', 'kraken', 'bkex', 'bitstamp', 'phemex'}
```
