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
