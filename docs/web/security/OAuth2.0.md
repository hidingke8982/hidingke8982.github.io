---
parent: Security
nav_order: 1
title: OAuth2.0
---

# OAuth2.0

OAuth 2.0은 인터넷 사용자들이 비밀번호를 제공하지 않고, 타사 어플리케이션(클라이언트)이 자신들의 정보에 제한적으로 접근할 수 있도록 허용하는 권한 부여 프레임워크. 사용자 인증(authentication)은 책임지지 않음.



## 주요 용어

- 인증(Authentication): 사용자가 누구인지 확인 (OAuth의 주목적은 아님)
- 인가 또는 권한 부여(Authorization): 사용자가 허가한 범위 내에서 자원 접근 허용
- Access Token: API에 접근할 수 있는 권한 토큰
- Refresh Token: Access Token 갱신용 토큰 (로그인 유지 등)



## 역할(Role)

| Type | Description |
|---|---|
| Resource Owner | 리소스 소유자 또는 사용자. 보호된 자원에 접근할 수 있는 자격을 부여해 주는 주체. OAuth2 프로토콜 흐름에서 클라이언트를 인증(Authorize)하는 역할을 수행한다. 인증이 완료되면 권한 획득 자격(Authorization Grant)을 클라이언트에게 부여한다. 개념적으로는 리소스 소유자가 자격을 부여하는 것이지만 일반적으로 권한 서버가 리소스 소유자와 클라이언트 사이에서 중개 역할을 수행하게 된다. |
| Client | 보호된 자원을 사용하려고 접근 요청을 하는 어플리케이션 |
| Authorization Server | 권한 서버. 클라이언트의 접근 자격을 확인하고 Access Token 발급 담당 (ex. Google) |
| Resource Server | 사용자의 보호된 자원을 호스팅하는 API 서버 (ex. Google API) |



## 권한 승인 방식(Grant Type)

| Type | Description |
|---|---|
| Authorization Code | 가장 보안이 높고 표준적, 웹 앱용 |
| Resource Owner Password Credentials | 사용자 ID/PW 직접 전달 |
| Client Credentials | 서버 간 인증, 사용자 없음 |
| Implicit | 현재는 권장되지 않음 (보안 취약), 브라우저 앱 용도였음 |


### Authorization Code Grant
![image](/assets/img/docs/web/authorization_code_grant.png)

### Resource Owner Password Credentials Grant
![image](/assets/img/docs/web/resource_owner_password_credentials_grant.png)

### Client Credentials Grant
![image](/assets/img/docs/web/client_credential_grant.png)

### Implicit Grant
![image](/assets/img/docs/web/implicit_grant.png)



## 추가 고려사항

- Access Token은 유출 시 위험하므로 HTTPS 사용 필수
- Refresh Token은 노출되지 않도록 주의
- OAuth 2.0 자체는 인증 프로토콜이 아니므로 OpenID Connect 같은 확장 필요



## 참조
- https://blog.naver.com/mds_datasecurity/222182943542
