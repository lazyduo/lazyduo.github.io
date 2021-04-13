---
title: "pyupbit"
date: 2021-04-13 21:23:00 +0900
categories: diary
---
## Upbit Class instance 생성

```python
import pyupbit

access_key = "xxx"
secret_key = "xxx"

upbit = pyupbit.Upbit(access_key, secret_key)
```

## Balance Check

```python
balance = upbit.get_balances()
print(balance)
```
결과는 아래와 같이 딕셔너리 리스트 형태로 얻어짐
```
[{'currency': 'KRW', 'balance': '5081.90606119', 'locked': '0.0', 'avg_buy_price': '0', 'avg_buy_price_modified': True, 'unit_currency': 'KRW'}, {'currency': 'BTC', 'balance': '0.00025324', 'locked': '0.0', 'avg_buy_price': '78584144.33', 'avg_buy_price_modified': False, 'unit_currency': 'KRW'}, {'currency': 'ETH', 'balance': '0.00174459', 'locked': '0.0', 'avg_buy_price': '2866000', 'avg_buy_price_modified': False, 'unit_currency': 'KRW'}, {'currency': 'XRP', 'balance': '3.48432055', 'locked': '0.0', 'avg_buy_price': '1435', 'avg_buy_price_modified': False, 'unit_currency': 'KRW'}, {'currency': 'MLK', 'balance': '1.55038759', 'locked': '0.0', 'avg_buy_price': '3225', 'avg_buy_price_modified': False, 'unit_currency': 'KRW'}]
```
