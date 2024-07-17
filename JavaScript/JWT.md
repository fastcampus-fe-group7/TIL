# JWT (JSON Web Token)
- 전자 서명된 URL-safe JSON으로, JSON의 변조를 체크할 수 있게 되어 있다.
- 서버와 클라이언트 간 정보를 주고 받을 때, http request header에 JSON토큰을 넣은 후 서버는 별도의 인증 과정 없이 헤더에 포함되어 있는 JWT정보를 통해 인증한다.
- JWT는 HMAC알고리즘을 사용하여 비밀키로 서명하거나, RSA를 이용한 Public Key/Private Key쌍으로 서명할 수 있다.

## JWT 토큰 구성
![JWT_Stacks](https://github.com/user-attachments/assets/964d0d39-00e9-45a1-bebb-a85d4e3a585f)

- JWT는 세 파트로 나누어진다.
- `헤더.페이로드.서명` 으로 구성된다.
- URI에서 파라미터로 사용할 수 있도록 Base64url 인코딩을 사용한다.
```
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6MTAwLCJlbWFpbCI6ImFubWluamlAY3ViZWl0LmNvbSIsImlhdCI6MTcyMTA3MTEyNSwiZXhwIjoxNzIxMDc0NzI1fQ.1wTYP-kErCuqYbEniV4SuPfGcB0_6Avj04FVCDPr7_M
```

### Header
- Header는 토큰의 타입과 해시 암호화 알고리즘으로 구성되어 있다.
- 첫번째는 토큰의 유형, 두번째는 해시 알고리즘을 나타낸다.
```JSON
{
  "alg": "HS256",
  "typ": "JWT"
}
```
### Payload
- Payload는 토큰에 담을 클레임(claim) 정보를 포함하고 있다.
- Payload에 담는 정보의 한 조각을 클레임이라 부르고 JSON처럼 name/value의 한 쌍으로 이루어져 있다.
- 여러개의 클레임을 담을 수 있다.
```JSON
{
  "id": 100,
  "email": "anminji@cubeit.com",
  "iat": 1721068281,
  "exp": 1721071881
}
```
### Signature
- Signature는 키를 포함하여 암호화되어 있다.
```javascript
HMACSHA256(
  base64UrlEncode(header) + "." +
  base64UrlEncode(payload),
  `SECRET-KEY` 
)
```

## 구현 예시 (로그인)
```javascript
// components/SignInForm/SignInForm.js - handleForm(event)
// components/API/AuthService.js - login(email, password, callback)
// server/index.js - Line.44
// server/index.js - generateToken(user)
```




## 디코딩하면 값을 알 수 있는데 왜 JWT를 사용할까?
- JWT는 자체적으로 토큰 유효성 검사가 가능하다. 
- 토큰이 위변조 되었는지만 확인하고, 위변조가 되지 않았으면 토큰 내부의 사용자 정보를 꺼내 사용할 수 있다.
- HMAC알고리즘과 공개/개인키를 모두 사용가능하기 때문에, 개인키 사용시 송신자가 누군지 알 수 있고, 공격자로 하여금 공격하기 더 어렵게 한다.
- 그렇기 때문에 디코딩 가능여부와 관계없이 위변조에 대한 신뢰가 있어 사용하는 것이다.

## 주의할 점
- HTTP 헤더를 통해 JWT 토큰을 보내는 경우 토큰이 너무 커지지 않도록 해야 한다. 
- 일부 서버는 8KB 이상의 헤더를 허용하지 않는다. 따라서 토큰에 너무 많은 정보를 포함하려고 하면 안된다.


## 참고자료
- [JWT.io](https://jwt.io/introduction)
- [JWT.io Debugger](https://jwt.io/#debugger-io)
- [jwt토큰 디코딩하면 페이로드 값을 다 아는데 왜 서명을 하는걸까? (HMAC알고리즘 동작방식)](https://giron.tistory.com/138)
- [코드참고 - 1차 토이프로젝트 6조](https://github.com/Dev-FE-1/idle-intranet-service)