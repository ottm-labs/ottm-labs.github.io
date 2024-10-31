# 결제

`window.overtake.payment`객체는 `PaymentHelper` 인스턴스를 사용하여 텔레그램 미니 앱에서의 Star 결제 기능 및 크립토 결제 기능을 제공합니다.
이 문서에서는 해당 객체의 인터페이스, 파라미터 설명, 호출 예제에 대해 안내합니다.

## 게임 아이템 Telegram Star 결제 요청

### 인터페이스
```javascript
window.overtake.star.requestPayment(gameId, productId, quantity, onSuccess?, onFail?);
```
### 파라미터
<b>requestPayment</b>

| 이름                 | 타입         | 설명                  | 예제 데이터                              |
|--------------------|------------|---------------------|-------------------------------------|
| gameId             | String     | 게임 식별자              | "OVERTAKE_MINIAPP"                  |
| productId          | String     | 제품 식별자              | "1234"                              |
| quantity           | Number     | 구매할 제품 수량           | 1                                   |
| onSuccess          | Function?  | 결제 성공 시 호출되는 콜백 함수	 | (id) => console.log(id)             |
| onFail             | Function?	 | 결제 실패 시 호출되는 콜백 함수  | (status, code) => alert(status)     |
| fetchPaymentStatus | Function?  | 결제 상태를 확인하기 위한 함수   | (invoiceId) => fetchPaymentStatus() |

<b>requestPayment.onSuccess</b>
결제 성공 시 호출되는 onSuccess 콜백 함수의 파라미터

| 이름        | 타입     | 설명    | 예제 데이터 |
|-----------|--------|-------|--------|
| invoiceId | String | 결제 ID | "1234" |

<b>requestPayment.onFail</b>
결제 실패 시 호출되는 onFail 콜백 함수의 파라미터

| 이름        | 타입     | 설명    | 예제 데이터   | 참고                                         |
|-----------|--------|-------|----------|--------------------------------------------|
| status    | Enum?  | 상태    | "failed" | ("pending", "paid", "cancelled", "failed") |
| errorCode | Number | 에러 코드 | 55016    | [결제 서버 에러 코드](결제-서버-에러-코드.md)              |


### 호출 예제
#### Typescript
```typescript
window.overtake.star.requestPayment(
  "OVERTAKE_MINIAPP", 
  "1234", 
  1, 
  (invoiceId) => console.log("Payment successful:", invoiceId), 
  (status, errorCode) => console.error("Payment failed:", status, errorCode),
);

```

#### C#
```csharp
StarRequestPayment(
    "OVERTAKE_MINIAPP", 
    "1234", 
    1, 
    invoiceId => Console.WriteLine($"Payment successful: {invoiceId}"), 
    (status, errorCode) => Console.WriteLine($"Payment failed: {status} - Error Code: {errorCode}")
);
```

## 게임 아이템 Cryptocurrency 결제 요청
이 함수는 주어진 게임과 상품에 대해 암호화폐 결제를 요청하는 역할을 합니다. walletProvider에 따라 지갑 앱을 열고 결제를 진행하며, fetchPaymentStatus가 제공된 경우 결제 상태를 확인하여 성공 또는 실패 콜백을 호출합니다.

### 인터페이스
```javascript
window.overtake.star.requestCryptoPayment(gameId, productId, productName, currencyId, quantity, walletProvider, onSuccess?, onFail?);
```
### 파라미터
<b>requestCryptoPayment</b>

| 이름              | 타입         | 설명                  | 예제 데이터                          | 참조                                                                                 |
|-----------------|------------|---------------------|---------------------------------|------------------------------------------------------------------------------------|
| gameId          | String     | 게임 식별자              | "OVERTAKE_MINIAPP"              |                                                                                    |
| productId       | String     | 제품 식별자              | "1234"                          |                                                                                    |
| productName     | String	    | 제품 이름               | 	"Legendary Sword"              | 상품쪽에선 다국어 처리를 하지 않기에, 결제 화면에서 결제하는 상품의 이름을 다국어 처리 하기 위해 전달합니다                      |
| currencyId	     | String     | 	결제 통화 식별자	         | "13473:null"                    | [게임의 상품 목록 조회에서 응답받는 id (api payload.contents.prices.currencyId)](게임의_상품_목록_조회.md) |
| quantity        | Number     | 구매할 제품 수량           | 1                               |                                                                                    |
| walletProvider	 | Enum       | 지갑 종류	              | "metamask"	                     | ("metamask", "okx")                                                                ||
| onSuccess       | Function?  | 결제 성공 시 호출되는 콜백 함수	 | (id) => console.log(id)         |                                                                                    |
| onFail          | Function?	 | 결제 실패 시 호출되는 콜백 함수  | (status, code) => alert(status) |                                                                                    |

<b>requestCryptoPayment.onSuccess</b>
결제 성공 시 호출되는 onSuccess 콜백 함수의 파라미터

| 이름        | 타입     | 설명    | 예제 데이터 |
|-----------|--------|-------|--------|
| invoiceId | String | 결제 ID | "1234" |

<b>requestCryptoPayment.onFail</b>
결제 실패 시 호출되는 onFail 콜백 함수의 파라미터

| 이름        | 타입     | 설명    | 예제 데이터    | 참고                            |
|-----------|--------|-------|-----------|-------------------------------|
| status    | Enum   | 상태    | "EXPIRED" | ("EXPIRED")                   |
| errorCode | Number | 에러 코드 | 55016     | [결제 서버 에러 코드](결제-서버-에러-코드.md) |

### 호출 예제
#### Typescript
```typescript
window.overtake.star.requestCryptoPayment(
  "OVERTAKE_MINIAPP", 
  "1234", 
  "Legendary Sword", 
  "13473:null", 
  1, 
  "metamask", 
  (invoiceId) => console.log("Payment successful:", invoiceId), 
  (status, errorCode) => console.error("Payment failed:", status, errorCode),
);


```

#### C#
```csharp
StarRequestCryptoPayment(
    "OVERTAKE_MINIAPP", 
    "1234", 
    "Legendary Sword", 
    "13473:null", 
    1, 
    "metamask", 
    invoiceId => Console.WriteLine($"Payment successful: {invoiceId}"), 
    (status, errorCode) => Console.WriteLine($"Payment failed: {status} - Error Code: {errorCode}")
);

```
