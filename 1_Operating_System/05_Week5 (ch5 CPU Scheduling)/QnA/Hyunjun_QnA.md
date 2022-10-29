# Ch5/4. CPU Scheduling & Thread 

<br>
<br>

## 김현준

<br>

### 1. CPU burst 시간 근사하는 법
OS가 CPU burst time을 예측하기 위해서는 기존에 사용되었던 동일한 프로세스의 사용시간을 기반으로 예측하게 된다. 이때 사용되는 식은 아래와 같다.

* Burst time(nth process) = alpha * actual burst time (n-1)th process + (1-alpha) * estimated burst time(n-1)th process 

이외에도 멀티 레벨 큐 스케쥴링처럼 프로세스의 종류를 나눔으로써 버스트 시간을 근사할 수 있다.
