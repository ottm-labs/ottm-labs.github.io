# 텔레그램 init data 검증

| 환경      | Host url                    |
|---------|-----------------------------|
| dev     | %public-api-base%      |
| testnet | %public-api-test-base% |
| prod    | %public-api-prod-base% |

<api-endpoint openapi-path="../../openapi/telegram_validation-swagger.json" method="POST" endpoint="/telegram/{gameId}/init-data/validate"/>