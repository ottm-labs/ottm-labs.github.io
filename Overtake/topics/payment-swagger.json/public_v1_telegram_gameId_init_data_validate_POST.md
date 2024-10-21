# 텔레그램 init data 검증

| 환경  | Host url                  |
|-----|---------------------------|
| dev | %public-api-base%/payment |
| prod| %public-api-prod-base%/payment |

<api-endpoint openapi-path="../../openapi/payment-swagger.json" method="POST" endpoint="/public/v1/telegram/{gameId}/init-data/validate"/>