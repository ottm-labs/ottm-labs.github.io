# Web Frontend 모듈

이 문서에서는 **Telegram Mini App**과 제공된 `ottm-payment-module.[version].js` 스크립트를 게임 애플리케이션에 통합하는 방법을 안내합니다.
먼저 아래 링크를 통해 모듈을 다운로드해 주세요.

## 0단계: 모듈 다운로드
[모듈 다운로드-prod](https://static.overtake.world/excluded-sync/modules/ottm-payment-module.v1.0.0.js)

[모듈 다운로드-testnet](https://static.overtake-test.world/excluded-sync/modules/ottm-payment-module.test.v1.0.0.js)

[모듈 다운로드-dev](https://static.ottm-dev.co/excluded-sync/modules/ottm-payment-module.dev.v1.0.0.js)


## 1단계: Telegram Web App SDK 추가

Telegram Web App 기능을 사용하려면 공식 Telegram Web App SDK를 포함해야 합니다. **다른 스크립트를 로드하기 전에** 아래의 스크립트 태그를 HTML 파일의 `<head>` 섹션에 추가해 주세요:

```html
<head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Telegram Mini App</title>
    <!-- place the script in the <head> tag before loading any other scripts -->
    <script src="https://telegram.org/js/telegram-web-app.js"></script>
</head>
```
## 2단계: 모듈 추가

Telegram Web App SDK를 로드한 후, (static 저장소에 업로드 된) (0) 번 절차에서 다운받은 js 파일을 <body> 섹션의 끝부분에 제공된 스크립트를 포함하세요:

```html
<body>
    <!-- html tags -->
    <script src="ottm-payment-module.v1.0.0.js"></script>
</body>
```

## 3단계: 모듈 인터페이스
`window.overtake` 객체는 세 개의 주요 인터페이스인 **StarPaymentHelper** **Web3ConnectHelper** **TelegramUtility** 를 포함하고 있습니다. 
이를 통해 사용자는 각각 텔레그램 정보조회, 스타 결제와 암호화폐 결제를 처리할 수 있습니다.

```typescript
window.overtake = {
  utils: TelegramUtility;
  star: StarPaymentHelper;
  web3Connect: Web3ConnectHelper;
  telegramInitData?: string;
  telegramUserId?: number;
};
```

### **StarPaymentHelper** 인터페이스
이 인터페이스는 Star 결제 처리와 관련된 기능을 제공합니다.

- **requestPayment(gameId, productId, quantity)**: 지정된 게임 ID, 상품 ID, 수량을 기반으로 결제를 요청합니다. 결제가 완료되면 생성된 인보이스 링크가 반환됩니다.

사용 예시:
```typescript
overtake.star.requestPayment(
  'GGS',
  '123',
  1
);
```

### **Web3ConnectHelper** 인터페이스
이 인터페이스는 암호화폐 결제를 지원하며, 다양한 지갑과의 상호작용을 제공합니다.

- **openMetaMaskApp(gameId, productId, currencyId, quantity, url)**: MetaMask 지갑을 사용하여 결제를 요청하는 함수입니다.
- **openOKXApp(gameId, productId, currencyId, quantity, url)**: OKX 지갑을 통해 결제를 요청하는 함수입니다.

사용 예시:
```typescript
window.overtake.web3Connect.openOKXApp("OVERTAKE_MINIAPP", "1234", "Gold Pack", "13473:0x3b2d8a1931736fc321c24864bceee981b11c3c57", 1);
```

```typescript
window.overtake.web3Connect.openMetaMaskApp("OVERTAKE_MINIAPP", "1234", "Gold Pack", "13473:0x3b2d8a1931736fc321c24864bceee981b11c3c57", 1);
```

## 예제 코드

다음은 위에서 설명한 스크립트를 포함한 HTML 예제입니다.
```html
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Telegram Mini App</title>
    <!-- 다른 스크립트 로드 전에 SDK를 포함 -->
    <script src="https://telegram.org/js/telegram-web-app.js"></script>
  </head>
  <body>
    <div id="app">
      <h1>Purchase Options</h1>
       <button onclick="overtake.star.requestPayment('GGS', '123', 1)">
        Star
      </button>
      <button
        onclick="overtake.web3Connect.openMetaMaskApp('GGS', '123', 'product name', '13473:null', 1)"
      >
        MetaMask(tIMX)
      </button>
      <button
        onclick="overtake.web3Connect.openOKXApp('GGS', '123', 'product name', '13473:null', 1)"
      >
        OKX(tIMX)
      </button>

    <!-- 스크립트를 body 끝에 포함 -->
    <script src="ottm-payment-module.v1.0.0."></script>
  </body>
</html>
