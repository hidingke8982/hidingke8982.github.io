---
parent: Architecture
nav_order: 1
title: WS-WAS-DB Architecture
---

# WS - WAS - DB 구조



## WS (Web Server)
웹 서버는 클라이언트(주로 웹 브라우저)로부터의 HTTP 요청을 수신하고, 정적 파일(HTML, CSS, JavaScript, 이미지 등)을 제공하거나, 동적 요청을 WAS(Web Application Server)로 전달하는 역할을 합니다.

- 주요 역할:
  - 정적 콘텐츠 제공: HTML, CSS, JavaScript 파일 제공.
    - HTML 파일: 웹 페이지의 구조를 정의.
    - CSS 파일: 웹 페이지의 스타일과 레이아웃을 정의.
    - JavaScript 파일: 웹 페이지의 동작과 인터랙션을 정의.
    - 이미지, 폰트, 비디오 등: 다양한 미디어 파일들.
  - 리버스 프록시: 동적 요청을 WAS로 전달하고, WAS 응답을 클라이언트에 반환.
  - 로드 밸런싱: 여러 대의 WAS로 트래픽을 분산.
  - 보안: SSL/TLS를 통한 HTTPS 설정, 방화벽, DDoS 방어.

- 대표적인 웹 서버:
  - Nginx: 고성능, 경량화된 웹 서버, 리버스 프록시 및 로드 밸런서로 자주 사용.
  - Apache HTTP Server: 다양한 모듈과 설정을 제공하는 유연한 웹 서버.
  - Caddy: 자동 HTTPS 설정과 간편한 구성 파일을 제공.



## WAS (Web Application Server)
WAS는 백엔드 애플리케이션 로직을 처리하고, 데이터베이스와 상호작용하는 서버입니다.

- 주요 역할:
  - 비즈니스 로직 처리: 애플리케이션의 핵심 기능 구현.
  - 데이터베이스 연동: 데이터 조회, 삽입, 수정, 삭제.
  - 세션 관리: 사용자 세션 추적 및 관리.
  - API 제공: RESTful API, GraphQL API 제공.

- 대표적인 Java 기반 WAS:
  - Spring Boot: 독립 실행형 애플리케이션 서버로 내장된 Tomcat을 제공.
  - Apache Tomcat: 자바 서블릿 및 JSP를 지원하는 애플리케이션 서버.
  - Jetty: 가볍고 유연한 자바 애플리케이션 서버.
  - JBoss/WildFly: 엔터프라이즈급 애플리케이션 서버.



## DB (데이터베이스)
데이터베이스는 애플리케이션의 데이터 저장소로, WAS가 필요로 하는 데이터를 저장하고 관리합니다.

- 주요 역할:
  - 데이터 저장: 사용자 정보, 상품 정보, 거래 내역 등을 저장.
  - 데이터 조회 및 조작: SQL 또는 NoSQL 쿼리로 데이터 조회, 삽입, 수정, 삭제.
  - 데이터 무결성 보장: 트랜잭션 관리 및 데이터 무결성 유지.

- 대표적인 데이터베이스:
  - 관계형 데이터베이스 (RDBMS):
    - MySQL, PostgreSQL, Oracle Database, Microsoft SQL Server.
  - NoSQL 데이터베이스:
    - MongoDB, Redis, Cassandra.



## 동작 흐름

1. 클라이언트 요청:
  - 사용자가 브라우저를 통해 특정 URL에 접근합니다.

2. WS 처리:
  - 정적 파일 요청인 경우, 웹 서버가 클라이언트에 직접 반환.
  - 동적 요청인 경우, WAS로 프록시합니다.

3. WAS 처리:
  - WAS가 요청을 받아 비즈니스 로직을 처리하고, DB와 상호작용합니다.
  - 처리된 결과를 웹 서버에 반환합니다.

4. WS 응답 전달:
  - 웹 서버가 WAS로부터 받은 응답을 클라이언트에 전달합니다.

5. 클라이언트 응답 렌더링:
  - 클라이언트는 받은 데이터를 바탕으로 웹 페이지를 렌더링합니다.



## 배포, 실행

### Backend

- 내장 서버(Spring Boot)
  - Spring Boot는 기본적으로 Tomcat, Netty, Jetty, Undertow 를 내장하고 있어, 독립 실행형 jar 파일로 실행 가능합니다.
  - 빌드: `mvn clean package` 또는 `gradle build` 을 통해 JAR 생성
  - 배포: `java -jar myapp.jar` 실행

- 외부 서버
  - 설정: pom.xml 또는 build.gradle에서 WAR 패키징 설정 
  - 빌드: `mvn clean package` 또는 `gradle build` 을 통해 WAR 생성 
  - 배포: 생성된 WAR 파일을 Tomcat의 webapps 폴더에 복사. Tomcat이 자동으로 애플리케이션을 로드하고 실행

### Frontend

- 빌드: 프론트엔드 개발자는 HTML, CSS, JavaScript 코드를 작성하고, 빌드 도구(예: Webpack, Parcel, Vite)를 사용하여 코드를 번들링하고 최적화합니다. 이 과정에서 코드가 압축(minification) 되고, 트랜스파일(transpiling) 되어 브라우저 호환성을 확보하게 됩니다.
- 배포: 빌드된 정적 파일(예: index.html, main.css, bundle.js)은 웹 서버에 배포
  - 직접 배포: 빌드된 파일을 Nginx 서버의 특정 디렉토리에 복사합니다. 
  - CDN 사용: 빌드된 파일을 CDN(Content Delivery Network)에 업로드하여 전 세계에 분산된 서버를 통해 제공.



## 장점

### 분리된 책임 (Separation of Concerns)
각 계층이 특정한 역할을 담당해 코드의 모듈화와 재사용성을 높입니다.

### 확장성 (Scalability)
웹 서버, WAS, DB를 각각 독립적으로 확장할 수 있습니다.

### 유지보수성 (Maintainability)
각 계층이 독립적으로 개발 및 배포될 수 있어, 유지보수가 용이합니다.
- CI/CD 파이프라인: Jenkins, GitLab CI, GitHub Actions 등을 사용해 자동화된 빌드, 테스트, 배포
- 컨테이너화: Docker를 사용해 애플리케이션과 웹 서버를 컨테이너로 패키징하고, Kubernetes 같은 오케스트레이션 도구로 관리 
- 버전 관리: Git과 같은 버전 관리 시스템을 통해 소스 코드 관리 및 배포

### 보안 (Security)
웹 서버가 외부 접근을 차단하고, WAS와 DB는 내부 네트워크에서만 접근 가능하게 할 수 있습니다.



## 추가 고려사항

### 캐싱 (Caching)
반복 요청에 대해 캐싱을 통해 서버 부하를 줄이고 응답 속도를 높일 수 있습니다.

### 로드 밸런싱 (Load Balancing)
여러 서버 인스턴스를 운영하여 트래픽을 고르게 분산시킬 수 있습니다.

### 컨테이너화 및 오케스트레이션
Docker와 Kubernetes를 사용하여 각 계층을 컨테이너로 패키징하고, 자동화된 배포 및 관리를 할 수 있습니다.

### 모니터링 및 로깅
각 계층의 성능과 상태를 모니터링하고 로그를 중앙 집중식으로 관리하여 장애를 신속히 파악하고 대응할 수 있습니다.
- 로그 관리: ELK 스택(Elasticsearch, Logstash, Kibana), Grafana, Prometheus 등을 사용해 로그와 메트릭을 수집하고 시각화
- 모니터링: New Relic, Datadog 등을 통해 애플리케이션의 성능과 상태를 실시간으로 모니터링



## 참조
- ChatGPT
