# Ch4/5. Thread & CPU Scheduling 

<br>
<br>

## 이재인
### 1. The Critical-section Problem
- Mutual exclution(상호배제) : 이미 한 프로세스가 critical-section에서 작업중일때 다른 프로세스는 critical section에 진입해서는 안된다.
- Progress(진행) : critical-section에서 작업중인 프로세스가 없다면 다른 프로세스가 critical-section에 진입할 수 있어야 한다.
- Bounded waiting(한정 대기) : critical-section에 진입하려는 프로게스가 무한하게 대기해서는 안된다.
Non-preemtive kernels(비선점 커널) 로 구현하면 critical-section문제가 발생하지 않지만, 비선점 스케줄링은 반응성이 떨어지기때문에 사용하지 않음.

### 2. Mutex locks
- Mutex locks은 여러 스레드가 공통 리소스에 접근하는것을 제어하는 기법으로, lock이 하나만 존재할수 있는 locking 매커니즘을 따름, 이미 하나의 스레드가 critical-section에서 작업중일때, 다른 스레드에서는 critical section에 진입할수 없음.
    - 즉, 프로세느는 critical-section에 접근하기전에 무조건 lock을 획득해야하고 빠져나올때 lock을 반환해야함.
    ![획득반환프로세스]https://imbf.github.io/assets/computer-science/synchronization-tools-7.png
