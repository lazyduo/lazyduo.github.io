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

## 잔고 조회
`get_balances()`**주의!** blance's'이다.

```python
balance = upbit.get_balances()
print(balance)
```
결과는 아래와 같이 딕셔너리의 리스트 형태로 얻어짐
```
[{'currency': 'KRW', 'balance': '5081.90606119', 'locked': '0.0', 'avg_buy_price': '0', 'avg_buy_price_modified': True, 'unit_currency': 'KRW'}, {'currency': 'BTC', 'balance': '0.00025324', 'locked': '0.0', 'avg_buy_price': '78584144.33', 'avg_buy_price_modified': False, 'unit_currency': 'KRW'}, {'currency': 'ETH', 'balance': '0.00174459', 'locked': '0.0', 'avg_buy_price': '2866000', 'avg_buy_price_modified': False, 'unit_currency': 'KRW'}, {'currency': 'XRP', 'balance': '3.48432055', 'locked': '0.0', 'avg_buy_price': '1435', 'avg_buy_price_modified': False, 'unit_currency': 'KRW'}, {'currency': 'MLK', 'balance': '1.55038759', 'locked': '0.0', 'avg_buy_price': '3225', 'avg_buy_price_modified': False, 'unit_currency': 'KRW'}]
```
참고로 s 없는 `upbit_balance()` 의 경우 해당 통화의 잔고만 선택적으로 보여줌.


## 지정가 매수/매도
 * 매수
```python
ret = upbit.buy_limit_order("KRW-XRP", 1000, 5)
print(ret)
```
원화시장에서 XRP(리플)을 지정가 1000원으로 5개 매수 요청!
return 결과는 아래와 같다.
```
{'uuid': 'eb0784d3-3d4f-42cc-9532-b6e009c3c099', 'side': 'bid', 'ord_type': 'limit', 'price': '1000.0', 'state': 'wait', 'market': 'KRW-XRP', 'created_at': '2021-04-13T21:03:53+09:00', 'volume': '5.0', 'remaining_volume': '5.0', 'reserved_fee': '2.5', 'remaining_fee': '2.5', 'paid_fee': '0.0', 'locked': '5002.5', 'executed_volume': '0.0', 'trades_count': 0}
```
결과값에서 **uuid**라는 unique ID가 리턴 되는 것을 주목.
error가 뜰 경우에는 아래와 같이 반환 된다.
```
{'error': {'message': '주문가능한 금액(KRW)이 부족합니다.', 'name': 'insufficient_funds_bid'}}
```
 * 매도
```python
ret = upbit.sell_limit_order("KRW-XRP", 5000, 3)
print (ret)
```
원화시장에서 XRP(리플)을 지정가 5000원으로 3개 매도 요청!
return 결과
```
{'uuid': 'ed390647-6205-49e4-b4c9-a57f89c33789', 'side': 'ask', 'ord_type': 'limit', 'price': '5000.0', 'state': 'wait', 'market': 'KRW-XRP', 'created_at': '2021-04-13T21:09:07+09:00', 'volume': '3.0', 'remaining_volume': '3.0', 'reserved_fee': '0.0', 'remaining_fee': '0.0', 'paid_fee': '0.0', 'locked': '3.0', 'executed_volume': '0.0', 'trades_count': 0}
```

## 주문 취소
아래와 같이 **uuid**를 argument로 해서 취소한다.
```python
ret = upbit.cancel_order('ed390647-6205-49e4-b4c9-a57f89c33789')
print(ret)
```
return 결과
```
{'uuid': 'ed390647-6205-49e4-b4c9-a57f89c33789', 'side': 'ask', 'ord_type': 'limit', 'price': '5000.0', 'state': 'wait', 'market': 'KRW-XRP', 'created_at': '2021-04-13T21:09:07+09:00', 'volume': '3.0', 'remaining_volume': '3.0', 'reserved_fee': '0.0', 'remaining_fee': '0.0', 'paid_fee': '0.0', 'locked': '3.0', 'executed_volume': '0.0', 'trades_count': 0}
```
