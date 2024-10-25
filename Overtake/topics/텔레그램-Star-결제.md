# 텔레그램 Star 결제

`window.overtake.star`객체는 `TelegramPaymentHelper` 인스턴스를 사용하여 텔레그램 미니 앱에서의 Star 결제 기능을 제공합니다.
이 문서에서는 해당 객체의 인터페이스, 파라미터 설명, 호출 예제에 대해 안내합니다.

> WIP: 결제의 상태(성공, 실패 등)를 받을 수 있는 콜백 추가 예정입니다.

## 게임 아이템 Star 결제 요청

### 인터페이스
```javascript
window.overtake.star.requestPayment(gameId, productId, quantity);
```
### 파라미터
<b>requestPayment</b>

| 이름        | 타입     | 설명        | 예제 데이터             |
|-----------|--------|-----------|--------------------|
| gameId    | String | 게임 식별자    | "OVERTAKE_MINIAPP" |
| productId | String | 제품 식별자    | "1234"             |
| quantity  | Number | 구매할 제품 수량 | 1                  |



### 에러 코드 및 메시지
| 코드      | 메시지                                                                 |
|---------|---------------------------------------------------------------------|
| 55005   | The game is not found.                                              |
| 55003   | The game detail is not found.                                       |
| 55004   | Unauthorized.                                                       |
| 55006   | The product is not found.                                           |
| 55007   | Purchase of the product in the requested currency is not available. |
| default | Unknown error.                                                      |


### 호출 예제
#### Typescript
```typescript
window.overtake.star.requestPayment("OVERTAKE_MINIAPP", "1234", 1);
```

#### C#
```csharp
StarRequestPayment("OVERTAKE_MINIAPP", "1234", 1);
```
