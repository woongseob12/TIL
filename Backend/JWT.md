# JWT

**JWT(Json Web Token)**: Json 포맷을 이용하여 사용자에 대한 속성을 저장하는 Claim 기반의 Web Token



**장점**

- 서버측 부하를 낮출 수 있음
  - 세션 정보를 유지할 필요가 없어 로드 밸런싱 환경에서 유리
- 별도의 인증 저장소 불필요
  - 사용자 인증에 필요한 모든 정보를 토큰 자체에 포함

**단점**

- 저장할 필드 수에 따라 토큰이 커질 수 있음
- 토큰이 거의 모든 요청에 대해 전송되므로 데이터 트래픽 크기에 영향을 미칠 수 있음



## 구조

- Header + Payload + Signature

- 각 부분을 `.`를 통해 구분

  ![image](https://user-images.githubusercontent.com/55429912/125617050-689aa96b-f6e3-41e6-aff5-816994051fef.png)



Header

```json
{
    "alg": "HS256",
    "typ": "JWT"
}
```

- Signature를 해싱하기 위한 알고리즘과 타입(JWT)



Payload

```json
{
    "sub": "1234567890",
    "name": "woongseob",
    "admin": true
}
```

- 데이터



Signature

```
HMACSHA256(
	base64UrlEncode(header) + "." + 
	base64UrlEncode(payload), secretKey)
```

- 인증



## 과정

![image](https://user-images.githubusercontent.com/55429912/125597563-6612d8c9-195b-48f6-8313-f7a0dbcff5c0.png)

