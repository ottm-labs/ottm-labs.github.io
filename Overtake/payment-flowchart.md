```mermaid
flowchart TB
game-ser[게임 서버]
subgraph miniapp
    game-cli[게임 클라이언트]
    jsmodule[오버테이크 js 모듈]
    game-cli -->|1 아이템 구매 기능 호출| jsmodule
end

subgraph 오버테이크 결제 시스템
	payment[오버테이크 결제 서버]
	sns[메시지 발송 시스템]
end
jsmodule <-->|2 결제 프로세스 진행| payment
payment -->|3 아이템 지급 요청 메시지 발신| sns
sns -->|4 아이템 지급 요청 메시지 전달| game-ser
jsmodule -->|5 아이템 지급 데이터 확인| game-ser
jsmodule -->|6 아이템 구매 종료 응답| game-cli

```