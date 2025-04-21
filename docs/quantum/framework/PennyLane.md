---
parent: Framework
nav_order: 2
title: PennyLane
---

# PennyLane
양자-고전(Quantum-Classical) 하이브리드 컴퓨팅, 양자 머신 러닝, 양자 화학을 위한 Python 라이브러리.  
양자 프로그래밍을 위한 오픈소스 프레임워크.



## 기능 및 특징
- 양자 컴퓨터 프로그래밍:  
  - 다양한 상태 준비(state preparation), 게이트(gates), 측정(measurements)을 사용하여 양자 회로를 구축 가능
  - 중간 회로 측정(mid-circuit measurements) 및 오류 완화(error mitigation)와 같은 고급 기능으로, 고성능 시뮬레이터 또는 다양한 하드웨어 장치에서 실행 가능
- 양자 알고리즘:
  - NISQ(소규모 양자 장치)부터 오류 보정이 가능한 양자 컴퓨팅까지 다양한 알고리즘 활용 가능 
  - 성능 분석, 회로 시각화, 양자 화학 및 알고리즘 개발을 위한 도구 제공
- 양자 하드웨어 및 시뮬레이터를 활용한 머신러닝:
  - PyTorch, TensorFlow, JAX, Keras, NumPy와 통합하여 하이브리드 모델을 정의하고 학습 가능 
  - 양자 최적화(quantum-aware optimizers) 및 하드웨어 호환 그래디언트(gradients) 지원
- 양자 데이터셋(Quantum datasets):
  - 고품질, 사전 시뮬레이션된 데이터셋을 활용하여 연구 시간을 단축하고 알고리즘 개발을 가속화
  - 데이터셋을 찾아보거나 직접 데이터를 기여할 수도 있음
- 컴파일 및 성능 최적화:
  - 실험적으로 JIT(Just-In-Time) 컴파일 지원
  - 전체 하이브리드 워크플로우를 컴파일 가능
  - 적응형 회로(adaptive circuits), 실시간 측정 피드백(real-time measurement feedback), 무제한 루프(unbounded loops)와 같은 고급 기능 지원



## 활용 분야
- 양자-고전 하이브리드 컴퓨팅
- 양자 머신러닝(QML)
    - TensorFlow, PyTorch 같은 딥러닝 프레임워크와 통합 가능
    - Variational Quantum Circuits (VQC) 기반으로 양자 머신러닝(Quantum Machine Learning, QML) 구현
- 양자 화학
- 양자 최적화
- 변분 양자 알고리즘(VQA)
- 자동 미분(Autograd, JAX, Torch) 가능



## 개발 환경
- 지원 언어
  - Python
- 지원 하드웨어
  - IonQ
  - Rigetti
  - Xanadu



## 예제 코드
```python
import pennylane as qml
import numpy as np

# 2-큐비트 양자 디바이스 (시뮬레이터)
dev = qml.device("default.qubit", wires=2)

@qml.qnode(dev)
def circuit(theta):
    qml.RY(theta, wires=0)
    qml.CNOT(wires=[0, 1])
    return qml.expval(qml.PauliZ(0))

theta = np.pi / 4
print(circuit(theta))  # 양자 회로 실행 결과 출력
```



## 장치(Device)와 플러그인(Plugin)

### 장치
장치는 양자 회로를 실행할 실제 하드웨어 또는 시뮬레이터를 나타낸다.   
즉, 장치는 양자 회로가 실제로 실행되는 대상을 의미한다. 
이를 통해 PennyLane은 사용자가 어떤 하드웨어나 시뮬레이터에서 회로를 실행할지 결정할 수 있다.

### 플러그인
플러그인은 PennyLane의 시스템에 하나 이상의 특정 장치가 포함될 수 있도록 해주는 소프트웨어 구성 요소다.  
즉, 플러그인은 장치가 PennyLane 환경에 통합되도록 해주는 패키지이다.
플러그인은 새로운 장치를 추가하거나 기존 장치의 기능을 확장하는 데 사용된다.

| 플러그인(패키지명)                                            | 장치                                                                                                | 설명                                                                                                                              | 백엔드                                      | 특징                                                                                                                   |
|-------------------------------------------------------|---------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------|------------------------------------------|----------------------------------------------------------------------------------------------------------------------|
| **Built-in (pennylane)**                              | **default.qubit**<br/>**default.mixed**<br/>**default.tensor**<br/>**default.kokkos**             | 상태 벡터(State Vector) 기반 기본 시뮬레이터<br/>밀도 행렬(Density Matrix) 기반 혼합 상태 시뮬레이터<br/>텐서 네트워크 기반 시뮬레이터<br/>Kokkos 라이브러리 기반 CPU/GPU 시뮬레이터 | CPU<br/>CPU<br/>CPU<br/>CPU & GPU        | 가장 기본적인 양자 회로 시뮬레이터<br/>노이즈 모델링 및 혼합 상태 시뮬레이션 가능<br/>많은 큐빗을 처리할 때 메모리 절약 가능<br/>멀티스레드 최적화 지원, 대규모 회로에 적합             |
| **Lightning (pennylane-lightning)**                   | **lightning.qubit**<br/>**lightning.mixed**<br/>**lightning.gpu**<br/>**lightning.kokkos**        | `default.qubit`보다 빠른 상태 벡터 기반 시뮬레이터<br/>`default.mixed`보다 빠른 혼합 상태 시뮬레이터<br/>CUDA 기반 GPU 시뮬레이터<br/>CPU/GPU 지원 Kokkos 기반 시뮬레이터   | CPU<br/>CPU<br/>GPU (CUDA)<br/>CPU & GPU | C++ 백엔드 사용, `default.qubit`보다 빠름<br/>`default.mixed`보다 성능 최적화됨<br/>GPU 가속 지원, 실시간 양자 회로 실행<br/>GPU 최적화, 대규모 회로 처리 가능 |
| **PennyLane-Qiskit (pennylane-qiskit)**               | **qiskit.aer**<br/>**qiskit.basicsim**<br/>**qiskit.remote**                                      |                                                                                                                                 |                                          | Qiskit                                                                                                               |
| **PennyLane-Braket (amazon-braket-pennylane-plugin)** | **braket.aws.qubit**<br/>**braket.local.qubit**<br/>**braket.aws.ahs**  <br/>**braket.local.ahs** |                                                                                                                                 |                                          | Amazon Braket                                                                                                        |
| **PennyLane-Cirq (pennylane-cirq)**                   | **cirq.simulator**<br/>**cirq.mixedsimulator**<br/>**cirq.qsim**<br/>**cirq.pasqal**              |                                                                                                                                 |                                          | Google Cirq                                                                                                          |
| **PennyLane-Q# (pennylane-qsharp)**                   | **microsoft.QuantumSimulator**                                                                    |                                                                                                                                 |                                          | Microsoft QDK                                                                                                        |
| **PennyLane-IonQ (pennylane-ionq)**                   | **ionq.simulator**<br/>**ionq.qpu**                                                               |                                                                                                                                 |                                          | IonQ                                                                                                                 |



## 참조
- ChatGPT
- https://pennylane.ai/plugins
