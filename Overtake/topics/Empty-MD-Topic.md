# 2024-11-01
## 결제
### 프론트 모듈
* StarPayment 및 Web3Connect 모듈을 Payment 모듈로 통합
* `requestPayment`, `requestCryptoPayment` 와 같은 결제 요청 함수 호출 시 성공 및 실패에 대한 callback 함수 받도록 수정
* telegramUtility 모듈에 텔레그램 내부에서 외부 브라우저로 링크 여는 `openLink` 함수 추가  

### 서버 연동
- 결제 서버 에러 코드 추가
- 서버 api 응답 예제 추가
- 사용자가 상품을 구매할 수 있는지 확인 api 추가