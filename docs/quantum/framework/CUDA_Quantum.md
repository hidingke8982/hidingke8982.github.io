---
parent: Framework
nav_order: 2
title: CUDA Quantum
---

# CUDA Quantum
NVIDIA 가 개발한 양자-고전 하이브리드 컴퓨팅 프레임워크.
![image](/assets/img/docs/quantum/NVIDIA_CUDA-Q.png)



## 기능 및 특징
- Software for Hybrid(Quantum-Classical) computing
- GPU 가속 기반으로 양자 시뮬레이션 & 하이브리드 알고리즘 실행
- NVIDIA DGX Quantum 시스템 및 GPU 가속 활용 가능
- 기존의 고전 컴퓨팅과 양자 컴퓨팅을 결합한 하이브리드 컴퓨팅에 초점 
- Qiskit, PennyLane과 달리 CUDA 및 GPU 활용에 최적화



## 활용 분야
- GPU 기반 양자 시뮬레이션 가속
- 양자 회로와 고전 알고리즘 결합 (하이브리드 양자 알고리즘)
- NVIDIA GPU 최적화 및 DGX Quantum 시스템과 통합



## 개발 환경
- 지원 언어
  - C++
  - Python
- 지원 하드웨어
  - NVIDIA GPU (DGX Quantum)



## 예제 코드
```python
import cudaq

# 2-큐비트 양자 회로 정의
@cudaq.kernel
def my_circuit():
    cudaq.h(0)       # 첫 번째 큐비트에 Hadamard 게이트 적용
    cudaq.cx(0, 1)   # CNOT 게이트 적용
    cudaq.mz(0)      # 측정
    cudaq.mz(1)

# 시뮬레이션 실행
result = cudaq.simulate(my_circuit)

# 결과 출력
print(result)
```



# cuQuantum
양자 시뮬레이터를 GPU 환경에서 실행할 수 있도록 만든 라이브러리
![image](/assets/img/docs/quantum/NVIDIA_cuQuantum.png)



## 특징
- Software (low-level libraries)



## 참조
- https://www.nvidia.com/en-us/
- https://www.nvidia.com/en-us/solutions/quantum-computing/
- https://www.nvidia.com/en-us/data-center/dgx-quantum/
- https://developer.nvidia.com/cuda-q
