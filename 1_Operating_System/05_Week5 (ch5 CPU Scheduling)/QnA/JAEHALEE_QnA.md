# Ch5/4. CPU Scheduling & Thread 

<br>
<br>

## 이재하

<br>

### 1. 1. Convoy Effect (호위 효과) 란?
- convoy effect란 여러 스레드가 서로 스케쥴링되는 환경에서, FCFS (First come first serviced)일 경우, 매우 올래 걸리는 프로세스기 할당될 경우, 다른 스레드들이 이러한 프로세스에 영향을 받아서 전체적인 시스템 utilization이 떨어지는 현상을 말한다.
- ![ConvoyEffect](https://images.velog.io/images/leeesangheee/post/be806447-d912-41a1-98f9-c5292202c3fc/4.png)
  - cf) FCFS 스케줄링이란?
    - 먼저 요청한 프로세스를 먼저 처리하는 방법
    - 비선점 스케줄링 (처리시간 도중 처리하던 프로세스를 멈추고 타 프로세스를 실행하지 않음)
    - EX) 피자를 먹고싶다면 차례대로 와서 줄을 서세요. 배가 얼마나 고프던, 피자를 얼마나 빨리 먹던 상관없이 선착순으로 피자를 드립니다.

