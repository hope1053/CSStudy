## ✔️ Race Condition이란?

- 공유 자원에 대해 여러 프로세스가 동시에 접근할 때, 공용 데이터에 대한 접근이 어떤 순서로 이루어졌는지에 따라 그 실행 결과가 같지 않고 달라지는 현상
- 자료의 일관성을 해치게 됨

## 👩‍💻 발생하게 되는 이유

- 커널 코드 실행 중에 인터럽트가 발생하는 경우
    - 커널이 가진 전역변수는 모든 프로세스의 공유물이므로 race condition이 발생할 수 있음
    - 커널 모드에서 작업하는 동안 인터럽트를 disable시켜서 인터럽트가 CPU제어권을 가져가지 못하게 하여 해결
- 프로세스가 시스템 콜을 하여 커널모드로 진입해서 작업을 수행하는 도중에 Context Switching이 발생하는 경우
    - 프로세스1이 커널모드에서 데이터를 조작하던 도중 시간이 초과되어 CPU제어권이 프로세스2로 넘어가 같은 데이터를 조작하는 경우
    - 시간이 초과되더라도 CPU 제어권이 다른 프로세스에게 넘어가지 않도록 해야 해결할 수 있음
- 멀티 프로세서에서 공유 메모리 내의 커널 데이터에 접근할 경우
    - 커널 내부에 있는 각 공유 데이터에 접근할 때마다 그 데이터에 대해 lock/unlock함으로써 해결할 수 있음

## ☑️ Critical Section(임계영역)

- 아무나 접근하지 못하도록 보호해야하는 부분
- 다중 프로그래밍 운영체제에서 여러 프로세스가 데이터를 공유하면서 수행될 때
**각 프로세스에서 공유데이터를 접근하는 프로그램 코드 부분**

## 👩‍💻 Race Condition 해결을 위해 충족해야하는 조건 3가지

### 🔥 Mutual Exclusion(상호 배제)

- 어떤 프로세스가 critical section을 수행 중이면 다른 모든 프로세스들은 그 임계 영역에 들어가지 못하게 막아야한다.

### 🔥 Progress(진행)

- critical section에 들어간 프로세스가 없다면 critical section에 들어가려는 프로세스가 있으면 들어가게 해주어야 한다.
- 즉, 임계영역에 있는 프로세스 외에는 다른 프로세스가 임계 영역에 진입하는 것을 방해하면 안된다.

### 🔥 Bounded Waiting(한정 대기)

- 프로세스들이 Critical Section에 진입하기 위해 무한정 대기해서는 안됨
- 기아(starvation) 상태를 방지하기 위해 프로세스가 critical section에 들어가려고 요청한 후부터 다른 프로세스들이 임계 영역에 들어가는 횟수에 한계가 있어야 한다. 임계 영역에 한 번 들어갔다 나온 프로세스는 다음에 들어갈 때 제한을 준다.
