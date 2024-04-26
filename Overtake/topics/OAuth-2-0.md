# OTTM<>게임사 - 멤버십

## **FLOW**

![OAuth2Authorize2.png](OAuth2Authorize2.png)

### OAuth 2.0 인증 코드 및 Access 토큰 발급

1. **OTTM OAuth 2.0 인증 서버로 redirect**
    - 요청
        - URL
            - 개발환경: %member-base%/auth/authorize
            - 상용환경: %member-prod-base%/auth/authorize
        - Parameter
            - scope (required)
                - 애플리케이션에서 액세스할 수 있는 리소스를 식별하는 공백으로 구분된 범위 목록
            - response_type (required)
                - OAuth 2.0 엔드포인트에서 승인 코드를 반환하는지 여부를 결정
                - ‘code’ 로 설정
            - redirect_uri (required)
                - 사용자가 인증 완료한 후 API 서버가 사용자를 redirect 하는 uri
                - 인증코드가 전송되는 uri
            - client_id (required)
                - 애플리케이션의 클라이언트 ID
            - state
                - 애플리케이션이 승인 요청과 승인 서버 응답 사이의 상태를 유지하는 데 사용하는 문자열 값
    - sample request

        ```
        %member-base%/auth/authorize?&scope=openid profile&response_type=code&state=xxx&redirect_uri=https://oauth2.example.com/code&client_id=xxx
        ```

    - sample response

        ```
        https://oauth2.example.com/code?&code=xxx&state=xxx
        ```


1. **Access 토큰 발급**
    - **Client Secret의 노출방지를 위해 외부의 접근이 통제된 서버에서 Access 토큰 발급**
    - 요청
        - METHOD
            - POST
        - URL
            - 개발환경: %api-base%/oauth2/v1/token
            - 상용환경: %api-prod-base%/oauth2/v1/token
        - Content-Type
            - application/x-www-form-urlencoded
        - BODY
            - grant_type
                - authorization_code로 설정
            - code
                - 인증코드 요청에서 반환된 인증 코드
            - client_id
                - 애플리케이션의 클라이언트 ID
            - client_secret
                - 애플리케이션의 클라이언트 SECRET
            - redirect_uri
                - 인증 코드 발급 받았던 uri
    - sample request

        ```
        curl -X POST \
        '%api-base%/oauth2/v1/token' \
        -d 'grant_type=authorization_code&code=xxx&client_secret=xxx&client_id=xxx&redirect_uri=https://oauth2.example.com/code'
        ```

    - sample response

        ```
        {
        	"access_token": "xxx",
          "refresh_token": "xxx",
          "scope": "openid profile",
          "id_token": "eyJraWQiOixxxxxxxxxxx.eyJzdWIiOiIxxxxxxxxxx.oqEvGYxxxxx",
          "token_type": "Bearer",
          "expires_in": 3599
        }
        ```


1. **Access 토큰 유효성 검사 및 회원 정보 조회**
    - 요청
        - METHOD
            - GET
        - URL
            - 개발환경: %api-base%/oauth2/v1/userinfo
            - 상용환경: %api-prod-base%/oauth2/v1/userinfo
        - HEADER
            - Authorization
                - Bearer {access_token}
    - sample request

        ```
        curl '%api-base%/oauth2/v1/userinfo' \
          -H 'Authorization: Bearer 2oPLZgMJ7tsZT6e1fDJfnog3RocUOD2f4e5Jua9QvgwBdKLlxhze86hMeblcPopH4XeXESezb1dInlQIGz5k7uA-TTP--r-cidmWX5gsQAby890sDVHC0n2VhZfvDHaF'
        ```

    - sample response

        ```
        {
          "sub": "e68a06bf9f2d4496882877cbecad27eb", // 회원의 unique id
          "nickname": "test",
          "email": "test@flask.global"
        }
        ```


## ERROR

- format

    ```
    {
      "error": {
        "code": "10076",
        "message": "Unauthorized oauth2 client"
      },
      "payload": null
    }
    ```

-

| code | message | Description | HTTP Status |
| --- | --- | --- | --- |
| 10051 | Invalid request | 요청이 잘못되었습니다 | 400 |
| 10071 | Invalid oauth2 scope | 요청한 scope 이 허용된 scope 이 아닙니다. | 400 |
| 10074 | Insufficient oauth2 scope | Access 토큰의 포함된 scope으로 해당 API를 호출 할 권한이 없습니다. | 400 |
| 10075 | Invalid oauth2 token | Access 토큰이 만료되었거나 형식 오류 또는 다른 이유로 유효하지 않습니다. | 400 |
| 10076 | Unauthorized oauth2 client | 등록된 client 의 grant type과 다른 요청을 했습니다. | 400 |