# 텔레그램 Star 결제

`window.overtake.star`객체는 `TelegramPaymentHelper` 인스턴스를 사용하여 텔레그램 미니 앱에서의 Star 결제 기능을 제공합니다.
이 문서에서는 해당 객체의 인터페이스, 파라미터 설명, 호출 예제에 대해 안내합니다.

## 타입
```typescript
type requestPaymentParams = {
  gameId: string;    
  productId: string;  
  quantity: number;   
};
```

## 게임 아이템 Star 결제 요청

### 인터페이스
```javascript
window.overtake.star.requestPayment({ gameId, productId, quantity });
```

### 에러 코드 및 메시지
| 코드        | 메시지                                                         |
|-----------|------------------------------------------------------------------------|
| 55005    | The game is not found.                                           |
| 55003 | The game detail is not found.                                                       |
| 55004  | Unauthorized.                                                           |
| 55006  | The product is not found.                                                 |
| 55007  | Purchase of the product in the requested currency is not available.                                                        |
| default  | Unknown error.                                            |


### 호출 예제
#### Typescript
```typescript 
window.overtake.star..requestPayment({
    gameId: "1234",
    productId: "5678",
    quantity: 1
  });
```

#### C# 
