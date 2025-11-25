---
parent: Development Platform
nav_order: 3
title: Overview
---

# Overview
양자 회로, 연산자, 기본 단위 수준에서 양자 컴퓨터를 사용하기 위한 오픈 소스 SDK.  
IBM 에서 개발한 양자 컴퓨팅 프레임워크.



## 기능 및 특징
- 양자 회로 설계 및 시뮬레이션
- IBM 양자 컴퓨터를 사용한 실험 가능
- 양자 알고리즘 연구
- 양자 소프트웨어 개발



## 개발 환경
- 지원 언어
  - Python
- 지원 하드웨어
  - IBM 양자 컴퓨터



## 예제 코드
```python
from qiskit import QuantumCircuit, Aer, transpile
from qiskit.visualization import plot_histogram
from qiskit.providers.aer import AerSimulator

# 2-큐비트 양자 회로 생성
qc = QuantumCircuit(2)
qc.h(0)  # 첫 번째 큐비트에 Hadamard 게이트 적용
qc.cx(0, 1)  # CNOT 게이트 적용
qc.measure_all()

# 시뮬레이터 실행
simulator = AerSimulator()
result = simulator.run(transpile(qc, simulator)).result()
counts = result.get_counts()

# 결과 시각화
plot_histogram(counts)
```


## 참조
- ChatGPT