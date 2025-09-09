---
parent: Virtualization
nav_order: 1
title: Overview
---

# Overview



## Virtual Machine(가상 머신)
가상 머신(Virtual Machine, VM)은 물리적 하드웨어 시스템에 구축되어 자체 CPU, 메모리, 네트워크 인터페이스 및 스토리지를 갖추고 가상 컴퓨터 시스템으로 작동하는 가상 환경입니다.   
이렇게 자체 컴퓨팅 자원과 OS를 갖춘 가상 컴퓨팅 환경을 가상 머신, Virtual Machine(VM)이라고 부른다. 
각 VM들은 같은 서버 위에 있을지라도 별도의 시스템처럼 동작한다. 
생성된 VM를 게스트 서버, VM들이 구동되는 서버를 호스트 서버라고 부른다.
<center><img src="/assets/img/docs/virtualization/virtualization.png" width="50%" height="50%"></center>

- 장점
  - 바이러스에 취약한 데이터에 접근하거나 새로운 개발 환경을 테스트하는 등의 위험한 작업을 해야 한다고 가정하자.
    호스트 OS에서 직접 작업하다가 잘못될 경우, 전체 시스템에 장애가 발생하거나 이전 환경으로 되돌릴 수 없는 상황이 생길 수 있다. 
    바로 이런 상황에서 VM을 유용하게 사용할 수 있다.
    VM은 격리된 환경을 제공하므로, VM 내에서 어떤 대상이 실행되든 다른 시스템을 방해하지 않는다. 
    또, 각 VM이 독립적인 OS를 갖기 때문에, 단일 서버에서 Windows, MAC, Linux 등 다양한 OS를 사용할 수도 있다. 
    유지/관리 및 자원 활용률 측면에서도 장점을 갖는다.
- 단점
  - VM이 많을수록 전통적인 방식 대비 성능의 안정성이 떨어지고 실행 속도가 느려진다. 
    아무래도 서버를 온전히 하나의 시스템으로 사용하는 것보다, 여러 가상 환경으로 분리하여 사용하는 것이 더 불안정할 수밖에 없다. 
    또한, Windows OS의 용량이 약 5GB 정도인 것을 고려하면, 모든 VM이 각각의 OS를 갖고 있는 것이 때로는 부담이 될 수도 있다. 
    이 점은 이후 등장하는 컨테이너와의 대표적인 차이점이 되기도 한다.
<center><img src="/assets/img/docs/virtualization/virtualization2.png" width="50%" height="50%"></center>



## Hypervisor(하이퍼바이저)
하이퍼바이저는 가상화 계층(Virtualization Layer)을 구현해주는 소프트웨어다. 
그림을 보면, 실물 하드웨어 자원들과 가상 머신들 사이의 'Virtualization Layer'이라는 가상화 계층이다.  
하이퍼바이저는 물리 하드웨어와 가상 머신의 영역을 분리하고 자신이 그 사이에서 중간 관리자, 즉 인터페이스 역할을 한다.
예를 들어, 하드웨어의 리소스를 가상 머신에 할당하고, 각 가상 머신의 리소스 사용을 스케쥴링하고, 가상 머신과 하드웨어 간의 I/O 명령을 처리하는 등의 역할을 하이퍼바이저가 담당한다. 
단일 서버에서 여러 개의 OS를 운영할 수 있는 것 또한 하이퍼바이저 덕분이다.
<center><img src="/assets/img/docs/virtualization/hypervisor.png" width="50%" height="50%"></center>

### Type1: Native(Bare-Metal) Hypervisor
하드웨어 위에서 직접 구동되어 게스트 OS를 관리한다. 
하드웨어에 OS를 설치하는 것처럼 하이퍼바이저를 설치하는 것이다.
- 특징
  - 유형 1은 호스트 OS가 따로 존재하지 않는다. 
  - 게스트 OS는 하드웨어 위에 2번째 수준으로 실행되기 때문에 오버헤드가 적다는 장점이 있다. 
  - 각 게스트 OS의 문제가 다른 게스트 OS에 영향을 주지 않는 것도 유형 1의 장점이다. 
  - 하지만, VM에 대한 자체적인 관리 기능이 없어, VM 관리를 위한 컴퓨터나 콘솔이 별개로 필요하다.
- 제품
  - VMware의 ESXi
  - Citrix의 Xen
  - Microsoft의 Hyper-V
<center><img src="/assets/img/docs/virtualization/hypervisor_type1.png" width="50%" height="50%"></center>

### Type2: Hosted Hypervisor
Host OS를 갖는 하이퍼바이저이다.
하드웨어에 호스트 OS 가 이미 설치되어 있고, 하이퍼바이저는 OS 위에서 소프트웨어로서 동작한다.
- 특징
  - 기존 시스템 위에서 쉽게 사용할 수 있다는 것이 유형 2의 가장 큰 장점이다.
  - 게스트 OS가 하드웨어 위에 3번째 수준으로 실행되기 때문에 오버헤드가 크고, 호스트 OS의 문제가 전체 게스트 OS에 영향을 줄 수 있다는 단점이다.
- 제품
  - VMware의 Workstation
  - Oracle의 VirtualBox
<center><img src="/assets/img/docs/virtualization/hypervisor_type2.png" width="50%" height="50%"></center>



## 참조
- ChatGPT
- https://selog.tistory.com/entry/%EA%B0%80%EC%83%81%ED%99%94-%EA%B0%80%EC%83%81%EB%A8%B8%EC%8B%A0VM%EA%B3%BC-%ED%95%98%EC%9D%B4%ED%8D%BC%EB%B0%94%EC%9D%B4%EC%A0%80-%EC%89%BD%EA%B2%8C-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0
- https://worlf.tistory.com/142
