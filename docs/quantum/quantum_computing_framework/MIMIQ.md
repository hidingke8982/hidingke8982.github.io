---
parent: Quantum Computing Framework
nav_order: 4
title: MIMIQ
---

# MIMIQ
양자 회로를 설계하고 원격 서비스에서 실행할 수 있게 해주는 양자 컴퓨팅 프레임워크.  
QPerfect 에서 개발한 범용 에뮬레이터.



## 기능 및 특징
- 최첨단 시뮬레이션과 압축 기술을 효율적으로 구현하여 작은 회로를 빠르게 에뮬레이션하고, 대규모 회로(최대 100~1000개 큐비트)를 정확하고 더 적은 리소스로 에뮬레이션할 수 있다.
- 워크플로를 방해하지 않고 여러 작업을 병렬로 실행할 수 있는 클라우드 인터페이스
- 대부분의 양자 회로를 처리할 수 있는 범용 Remote 에뮬레이터
- 회로 구성을 위한 고급 기능(노이즈, 조건 논리, 중간 회로 측정 등)의 전문가용 세트에 대한 액세스 가능
- 전체 양자 상태 속성(상태 진폭, 기대 값, 얽힘 측정 등)에 대한 액세스 가능
- 시뮬레이션 알고리즘
  - State Vector: 소규모 회로에서 완벽하게 정확한 시뮬레이션
  - MPS(Matrix Product State): 통제되고 투명한 충실도 지표를 갖춘 대규모 시뮬레이션



## 개발 환경
- 지원 언어
    - Python
- 지원 하드웨어
    - 자체 Remote 에뮬레이터



## 예제 코드
```python
from mimiqcircuits import *
from mimiqcircuits.visualization import plothistogram

# MIMIQ 서버 연결
conn = MimiqConnection()
conn.connect("your_account", "your_password")

print("Connected: ", conn.isOpen, "\n")

# N개의 큐비트를 사용하는 회로 생성
circuit = Circuit()
num_of_qubits = 10
# type_algorithm = "statevector"
type_algorithm = "mps"

# 모든 큐비트에 Hadamard 게이트 적용
for q in range(num_of_qubits):
    circuit.push(GateH(), q)

# 일부 큐비트에 CNOT 게이트 적용 (짝수 -> 홀수 연결)
for q in range(0, num_of_qubits-1, 2):
    circuit.push(GateCX(), q, q + 1)

# 특정한 큐비트 페어에 대해 기대값 계산
circuit.push(ExpectationValue(Projector11()), 0, num_of_qubits-1, 0)

# 모든 큐비트 측정
circuit.push(Measure(), range(num_of_qubits), range(num_of_qubits))

# 노이즈 추가 (Amplitude Damping)
for q in range(num_of_qubits):
    circuit.add_noise(GateH(), AmplitudeDamping(0.01))

print("Executing...\n")
job_execution_id = conn.execute(circuit, algorithm=type_algorithm)
print("Running job: ", job_execution_id, "\n")

# 결과 가져오기
qsc_result = conn.get_result(job_execution_id)
print("Complete: \n", qsc_result, "\n")

# 결과 출력 및 시각화
qsc_result.histogram()
plothistogram(qsc_result)
```



## 참조
- https://docs.qperfect.io/mimiqcircuits-python/mimiq_documentation.html
