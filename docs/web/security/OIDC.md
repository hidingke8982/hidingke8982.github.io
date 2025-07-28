---
parent: Security
nav_order: 2
title: OIDC
---

# OIDC (OpenID Connect)

OIDC는 OAuth 2.0 기반에 인증 기능을 명확하게 확장한 프로토콜. 포함관계라고 보면 됌. “OIDC를 쓴다”는 말은, 인증 프로토콜로 OIDC를 사용하며, 그 기반 인프라로 OAuth 2.0 인가 프로토콜을 사용한다는 뜻.

- OAuth 2.0의 access_token 외에 id_token (JWT 형식)을 추가로 발급하여 사용자의 신원 정보도 제공
- 사용자 로그인, SSO(Single Sign-On) 등에 활용
- scope=openid 로 명시하면 OIDC 흐름


## 예시

“사용자가 Google 계정으로 로그인하고, 그 사용자가 Google Drive를 읽을 권한도 줌”

- OIDC: 로그인 (사용자 신원 확인, id_token 발급)
- OAuth 2.0: 권한 부여 (access_token 발급 후 Drive API 접근)



## 참조
- https://en.wikipedia.org/wiki/Identity_provider
