# Ch4/5. Thread & CPU Scheduling 

<br>
<br>

## 이재인
### 1. Preemptive vs Non-preemptive

- Preemptive(선점)
    - 프로세스가 CPU를 점유하고 있는 동안 I/O나 인터럽트가 발생한것도 아니고 모든 작업을 끝내지도 않았는데, 다른프로세스가 해당 CPU를 강제 점유 할 수 있다.
    즉, 프로세스가 정상적으로 수행중인 가운데 다른 프로세스가 CPU를 강제로 점유하여 실행할수 있다.
- Non-preemptive(비선점)
    - 한 프로세스가 한번 CPU를 점유했다면, I/O 또는 프로세스가 종요될때까지 다른 프로세스가 CPU를 점유하지 못함.
ref. https://velog.io/@codemcd/%EC%9A%B4%EC%98%81%EC%B2%B4%EC%A0%9COS-6.-CPU-%EC%8A%A4%EC%BC%80%EC%A4%84%EB%A7%81

### 2. CPU Burst vs I/O Burst

- CPU 버스트
    - CPU 명령을 실행하는것
- I/O 버스트
    - I/O를 요청한 다음 기다리는 시간.
ref. https://jhnyang.tistory.com/25
