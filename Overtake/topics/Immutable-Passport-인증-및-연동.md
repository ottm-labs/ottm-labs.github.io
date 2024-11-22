# Immutable Passport 인증 및 연동

# Immutable Passport 로그인 및 로그아웃
이 문서는 Immutable Passport를 사용하여 사용자가 Web3 기반 애플리케이션에 로그인하고 로그아웃할 수 있도록 구현하는 방법을 설명합니다.


## 모듈 인터페이스
```javascript
window.overtake = {
    web3Connect: Web3ConnectHelper
};
```

## Immutable Passport 로그인 (Sign-In)
Immutable Passport를 사용하여 사용자가 Web3 애플리케이션에 로그인하고, 인증된 사용자 주소를 반환합니다.
이 과정에서 서버는 제공된 ID 토큰을 검증하여 사용자의 인증 상태를 확인합니다.

### 인터페이스
```javascript
window.overtake.web3Connect.signInWithPassport(gameId, onSuccess?, onFail?);
```

### 파라미터
<b>signInWithPassport</b>

| 이름                 | 타입         | 설명                  | 예제 데이터                         |
|--------------------|------------|---------------------|--------------------------------|
| gameId             | String     | 게임 식별자              | "OVERTAKE_MINIAPP"             |
| onSuccess          | Function?  | 로그인 성공 시 호출되는 콜백 함수		 | (userAddress) => console.log(userAddress) |
| onFail             | Function?	 | 로그인 실패 시 호출되는 콜백 함수  | (errorCode) => alert(errorCode) |

<b>signInWithPassport.onSuccess</b>
로그인 성공 시 호출되는 onSuccess 콜백 함수의 파라미터:

| 이름        | 타입     | 설명                  | 예제 데이터 |
|-----------|--------|---------------------|--------|
| userAddress | String | 인증된 사용자의 지갑 주소 | "0x1234abcd5678ef90..." |

<b>signInWithPassport.onFail</b>
로그인 실패 시 호출되는 onFail 콜백 함수의 파라미터:

| 이름        | 타입     | 설명    | 예제 데이터   | 참고                                                          |
|-----------|--------|-------|----------|-------------------------------------------------------------|
| errorCode | Number | 에러 코드 | 55016    | [클라이언트 에러 코드](클라이언트-에러-코드.md) |


### 호출 예제
#### Typescript
```typescript
overtake.web3Connect.signInWithPassport('OVERTAKE_MINIAPP',
(userAddress) => alert(`User address: ${userAddress}`),
(errorCode) => alert(`Login failed with error code: ${errorCode}`));
```

#### C#
```csharp
signInWithPassport(
    "OVERTAKE_MINIAPP", 
    (userAddress) => Console.WriteLine($"User address: {userAddress}"), 
    (errorCode) => Console.WriteLine($"Login failed with error code: {errorCode}")
);
```



## Immutable Passport 로그아웃 (Sign-Out)
Immutable Passport를 사용하여 사용자의 세션을 종료합니다.

### 인터페이스
```javascript
window.overtake.web3Connect.signOutWithPassport(onSuccess?, onFail?);
```

### 파라미터
<b>signOutWithPassport</b>

| 이름                 | 타입         | 설명                  | 예제 데이터                         |
|--------------------|------------|---------------------|--------------------------------|
| onSuccess          | Function?  | 로그아웃 성공 시 호출되는 콜백 함수		 | (result) => console.log(result) |
| onFail             | Function?	 | 로그아웃 실패 시 호출되는 콜백 함수  | (errorCode) => alert(errorCode) |

<b>signOutWithPassport.onSuccess</b>
로그아웃 성공 시 호출되는 onSuccess 콜백 함수의 파라미터:

| 이름        | 타입     | 설명                  | 예제 데이터 |
|-----------|--------|---------------------|--------|
| result | Boolean | 로그아웃 성공 여부 | true |

<b>signOutWithPassport.onFail</b>
로그아웃 실패 시 호출되는 onFail 콜백 함수의 파라미터:

| 이름        | 타입     | 설명    | 예제 데이터   | 참고                                                           |
|-----------|--------|-------|----------|--------------------------------------------------------------|
| errorCode | Number | 에러 코드 | 55016    | [결제 서버 에러 코드](결제-서버-에러-코드.md), [클라이언트 에러 코드](클라이언트-에러-코드.md) |


### 호출 예제
#### Typescript
```typescript
overtake.web3Connect.signOutWithPassport(
(result) => alert(`Sign out successful: ${result}`),
(errorCode) => alert(`Sign out failed with error code: ${errorCode}`)
);
```

#### C#
```csharp
signOutWithPassport(
    (result) => Console.WriteLine($"Sign out successful: {result}"), 
    (errorCode) => Console.WriteLine($"Sign out failed with error code: {errorCode}")
);
```
