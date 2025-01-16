### CPU 스케줄링

### CPU 스케줄링이란 무엇이며, 주요 알고리즘에는 어떤 것들이 있나요?

- **CPU 스케줄링**은 프로세스들이 CPU를 효율적으로 사용할 수 있도록 CPU 사용 순서를 결정하는 기법입니다.
- **주요 알고리즘**:
  1. **FCFS (First-Come, First-Served)**: 먼저 도착한 프로세스를 먼저 실행
  2. **SJF (Shortest Job First)**: 실행 시간이 가장 짧은 프로세스를 먼저 실행
  3. **Round Robin (RR)**: 각 프로세스가 일정 시간 단위(time quantum) 동안 CPU를 사용
  4. **Priority Scheduling**: 우선순위에 따라 프로세스 실행
  5. **Multilevel Queue Scheduling**: 여러 큐로 프로세스 분류 후 큐 별 스케줄링

### Preemptive Scheduling과 Non-Preemptive Scheduling의 차이점

- **Preemptive Scheduling**:
  - 실행 중인 프로세스가 중단될 수 있음.
  - 응답 시간이 중요할 때 사용.
  - 예: Round Robin, Priority Scheduling(Preemptive)
- **Non-Preemptive Scheduling**:
  - 프로세스가 끝날 때까지 CPU 점유.
  - 간단하지만 응답 시간이 길어질 수 있음.
  - 예: FCFS, SJF

### 멀티레벨 큐 스케줄링(Multi-level Queue Scheduling)

- 프로세스를 여러 우선순위 큐로 나눔.
- 각 큐는 서로 다른 스케줄링 알고리즘을 사용할 수 있음.
- 높은 우선순위 큐에서 작업이 끝날 때까지 낮은 우선순위 큐는 대기.

### 멀티레벨 큐 스케줄링의 장점

- 단순성과 효율성:
  큐를 나누어 프로세스의 특성에 맞게 처리.
- 유연성:
  각 큐에서 독립적인 스케줄링 알고리즘 사용 가능.
  다양한 작업 처리 가능:
  우선순위가 다른 작업을 효율적으로 처리.

### 멀티레벨 큐 스케줄링의 단점

**기아 문제 (Starvation):** 낮은 우선순위 큐의 작업이 높은 우선순위 큐의 작업에 의해 무한히 대기 가능.

- 해결 방법: **에이징(Aging)**을 적용해 낮은 우선순위 작업의 우선순위를 점진적으로 높임.

**복잡성**: 큐 간의 우선순위와 시간 분배를 설계하는 데 복잡성이 추가.

**고정 우선순위 구조:** 우선순위가 고정되어 있어 유동적인 작업 변화에 적응하기 어려움.

## 멀티레벨 큐 스케줄링

### 데이터베이스 관리 시스템 (DBMS)

- DBMS는 쿼리 우선순위에 따라 작업을 분리해 처리.
- **예:**
  긴급 쿼리(트랜잭션): 높은 우선순위 큐.
  배치 작업(보고서 생성): 낮은 우선순위 큐.

### 컨테이너 오케스트레이션 (Kubernetes)

- Kubernetes의 스케줄링 정책에서 작업을 우선순위 클래스로 분류.
- 긴급 작업(Priority Class)과 일반 작업을 분리해 처리.