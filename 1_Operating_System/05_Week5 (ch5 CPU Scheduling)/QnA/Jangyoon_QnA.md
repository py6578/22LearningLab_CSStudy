# Ch 5. CPU Scheduling 

<br>
<br>

### 1. RR (Round-Robin) Scheduling 이란?
- 프로세스가 동작할 시간 단위 시간 'Time slice' 할당하여 스케쥴링을 구현한다.
- CPU 버스트가 Time slice를 넘길경우, OS에 인터럽트가 발생하여 실행중인 프로세스는 준비 큐에 들어가데 된다.
- 경험적으로, CPU 버스트의 80% 정도가 Time slice에 비해 짧은 시간을 가지는 것이 좋다.

<br>
<br>

### 2. RR Scheduling이 다단계 큐 스케쥴링에서 어떻게 활용되는가?
- 다단계 큐 스케쥴링은 우선순위에 대한 각각의 준비 큐가 존재한다.
- 각각의 큐에서 RR 알고리즘을 통해 프로세스들이 Time slice를 할당받아 실행된다.
- 만약 우선순위가 가장 높은 준비 큐 내의 프로세스가 전부 실행된다면, 다음 우선순위의 큐에서 반복된다.