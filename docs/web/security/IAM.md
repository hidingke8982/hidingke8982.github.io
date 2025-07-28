---
parent: Security
nav_order: 3
title: IAM
---

# IAM (Identity and Access Management)

사용자(기업에 연결되거나 기업 내부에 연결된 생태계의 일부)가 기술 자원에 대한 적절한 액세스 권한을 갖도록 보장하는 정책 및 기술의 프레임워크이다. 구성 단계에서 액세스 권한을 먼저 등록하고 승인한 다음, 운영 단계에서 이전에 승인된 액세스 권한에 따라 애플리케이션, 시스템 또는 네트워크에 액세스할 수 있는 개인이나 그룹을 식별, 인증 및 제어하는 ​​조직적 및 기술적 프로세스이다.



## 기능

- Pure identity function: 액세스 또는 권한에 관계없이 ID를 생성, 관리 및 삭제합니다.
- User access function: 예를 들어, 고객이 서비스에 로그인하는 데 사용하는 스마트 카드 및 관련 데이터(전통적인 관점)
- Service function: 사용자와 그 장치에 개인화된 역할 기반 온라인 주문형 멀티미디어(콘텐츠), 존재 기반 서비스를 제공하는 시스템
- Identity federation: 비밀번호를 알지 못해도 사용자를 인증하기 위해 연합 ID 에 의존하는 시스템
- Audit function: 병목 현상, 오작동 및 의심스러운 동작을 모니터링합니다.



# KeyCloak

Open Source IAM(Identity and Access Management) 솔루션이자, OAuth 2.0 & OIDC 스펙이 적용된 IdP(Identity Provider) 이다.



## 기능

- Identity Management
    - 사용자 등록 및 프로필 관리
    - 그룹/조직 구성원 관리
    - 이메일/전화 기반 사용자 속성 관리
- Access Management
    - Realm 단위 격리
    - 클라이언트 앱 별 권한 설정
    - Role, Group, Permission 기반 제어
- Authentication
    - OIDC 기반 로그인
    - MFA 지원 (OTP, WebAuthn 등)
    - 브라우저 기반 SSO
- Authorization
    - OAuth 2.0 기반의 확장된 정책 기반 접근 제어(RBAC) 제공
    - Fine-grained Resource Access 정책 설정 가능
- Audit / Admin 기능
    - 관리자 콘솔 UI
    - 사용자 활동/로그 기록
    - REST API 기반 자동화 가능



## 참조
- https://en.wikipedia.org/wiki/Identity_and_access_management 
