---
title: Jupyter
parent: Tool
nav_order: 1
---

# Jupyter



## JupyterNotebook
인터랙티브한 문서 형태로 Python, R, Julia 등 다양한 언어의 코드를 실행할 수 있는 환경입니다. 코드, 결과, 설명, 시각화를 한 파일(.ipynb)에 담아 작업할 수 있습니다.
- 특징
  - 웹 브라우저 기반. 
  - 데이터 분석 및 공유에 적합. 
  - Markdown 지원. 
  - 실행된 결과를 저장 가능.

### .ipynb 파일 실행 과정
1. JupyterLab 실행
    - cmd 에서 명령어로 실행
    - 로컬 서버가 실행되고, 웹 브라우저에서 인터페이스가 열림
2. .ipynb 파일 생성 및 열기
3. 커널 연결
    - 특정 언어의 코드를 실행하는 백그라운드 프로세스
        - 파이썬 커널의 경우, 일반적인 Python 의 실행구조(CPython, PVM(Python Virtual Machine))을 포함하고 있고, JupyterLab 과 통신하기 위해 추가적인 기능을 제공함.
        - CPython 에서 바이트코드로 변경 후, PVM 이 바이트코드를 한 줄씩 기계어로 번역해 실행 함
    - JupyterLab 은 언어를 감지해 적절한 커널을 자동으로 연결시켜 줌
    - 커널을 선택하거나 교체 가능
4. 코드 실행
    - 사용자가 셀을 선택하고 실행
    - 커널이 셀의 코드를 처리하고 결과를 반환
    - 결과는 셀 아래에 표시
5. 출력과 시각화
6. 결과 저장
7. 커널 관리
8. 파일 종료 및 서버 중지



## JupyterLab
Jupyter Notebook 의 차세대 인터페이스로, IDE(통합 개발 환경)와 비슷한 방식으로 다중 창, 파일 탐색기, 터미널 등을 지원합니다.
- 특징
  - 유연한 UI(다중 탭, 패널 분할 등).
  - Jupyter Notebook과 호환.
  - 확장 플러그인으로 기능 확장 가능.
  - 파일 관리, 실시간 협업 지원.



## JupyterHub
여러 사용자를 지원하는 Jupyter Notebook 환경으로, 조직이나 팀이 공동으로 사용할 수 있습니다. 
- 특징
  - 일종의 동적 WAS 라고 할 수 있다. 
  - 사용자 인증 및 관리.
  - 서버에서 호스팅되어 다수의 사용자가 동시에 작업 가능.
  - 교육, 연구, 협업에 적합. 
  - Docker 및 Kubernetes 와 연동 가능.
- 아키텍처
  - HTTP Server
    - 8000번 포트로 접근하면 JupyterHub 인터페이스 페이지가 뜬다.
  - Spawner
    - 각 사용자의 JupyterLab 환경을 생성하는 컴포넌트다. Local Process(default), Docker, K8s 로 설정이 가능하다.
    - Docker 로 설정했을 경우, 각 사용자마다 JupyterLab 이 Container 로 실행된다. Docker image 는 JupyterNotebook 기반 이미지를 미리 pull 받아놓고, 설정 파일에 이 이미지를 설정해야 한다.
  - Authenticator
  - Proxy
    - Reverse proxy 로 동작하며, 각 사용자의 JupyterLab 세션으로의 연결을 관리한다.

    
    
## Jupyter Enterprise Gateway
(내용 필요)



---
## 참조
- ChatGPT
- https://blog.jupyter.org/introducing-jupyter-enterprise-gateway-db4859f86762
- https://github.com/jupyter-server/enterprise_gateway
- https://jupyter-enterprise-gateway.readthedocs.io/en/latest/
