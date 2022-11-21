# Ch5/4. CPU Scheduling & Thread 

<br>
------
<br>

## 박예리

<br>

### 1. Priority Scheduling의 정의, 문제점, 해결점
`Priority scheduling은 여러개의 프로세스가 Ready Queue에 존재할 때, 각 프로세스가 우선순위에 따라 CPU Scheduling 순서가 정렬되는 Preemptive Scheduling  방법이다.  
Preemptive Scheduling 이므로 지금 CPU가 수행 중인 프로세스(A)보다 더 높은 순위의 프로세스(B)가 등장하면 수행 중이었던 프로세스는 CPU Control를 B에게 넘겨주게 된다. (Context Switching)
그렇기 때문에 `우선순위가 낮은 프로세스가 더 높은 우선순위의 프로세스들에게 밀려 영영 실행되지 않는 Starvation 문제`가 존재한다. 
(책에 의하면 이 starvation 프로세스는 새벽 2시에 실행되거나 몇년 뒤에도 실행이 안되는 무서운 경우도 있다고,,,)
이를 해결하기 위한 방법으로 낮은 우선순위의 프로세스라도 `해당 프로세스의 Wait time이 길어지면 해당 프로세스의 우선순위를 높여 줌`으로써 우선순위에 밀려 실행되지 않는 프로세스가 없도록하는 Aging 기법이 있다.

    #### 1-1. Round Robin 에서의 Starvation / Preepmtion Scheduling 문제
    : Round Robin 는 기준 시간을 기준(Tq)으로 그 전에 프로세스 끝난다면 FCFS(First Come, First Serve)처럼 동작하지만, 실행시간이 Tq보다 늘어난다면 Timeout 되어 CPU control을 반납하고 Ready Queue 가장 뒤로 들어가는 Scheduling 방법이다.  
    시간을 기준으로 선점 방식이 정해지므로, Preemption Scheduling 이라 할 수 있고, 이로 인해 프로세스 시간이 긴 프로세스의 경우 계속해서 밀려나가 Starvation 문제에 직면할 수도 있다고 생각이 든다.

        #### => 이렇게 수행시간을 미리 예측하여 수행 시간의 길이에 따라 스케쥴링을 할 수 있는 원리가 무엇인가? : 수행 전 수행시간에 대한 예측?
        - (TBD) 과거 수행 시간의 기록을 누적하여 다음 시간을 예측하는 A(t+1) = B(t-1) + C(t) 과거 시간을 보는 모델링이 있을 수 있을 것 같고,
        - 대체적으로 짧은 시간의 프로세스가 많고, 긴 시간의 프로세스는 적은 평균을 참조할 수 있다. 
        ![https://www.cs.uic.edu/~jbell/CourseNotes/OperatingSystems/images/Chapter6/6_02_CPU_Histogram.jpg](https://www.cs.uic.edu/~jbell/CourseNotes/OperatingSystems/images/Chapter6/6_02_CPU_Histogram.jpg)
        - 프로세서 제조사가 여러 프로세스에 따른 수행시간에 대한 데이터가 존재하여 대략적으로 예측하는 값이 모델링 값이 존재할 것 같다
    
<br>
<br>

### 2. Preemption Scheduling 의 문제점?
Preeption Scheduling은 해당 프로세스가 수행 중에 다른 프로세스가 왔을 때 수행 줃인 프로세스로부터 CPU의 control을 앗아 다른 프로세스에게 전달할 수 있는 선점적 스케줄링을 의미한다.
이때 선점 기준에 따라 `Race Condtion이 발생하여, 둘 중 어떤 프로세스가 먼저 실행될 지 모를 수 있기 때문에 Data의 손실이나, 변경이 발생`할 수 있다.
이렇기 때문에 동시 접근하면 위험한 데이터에 한해 `Mutex를 통해 해당 영역에 대한 동시접근`을 막고, `이 영역의 시작과 끝에서는 Interrupt가 일어나지 않도록` 막는다.
이렇게 Mutex로 보호한 코드 block의 경우 interrupt가 불가능하기 때문에 Context switching이 불가능하고, 이는 곧 `Multithreading이 중단`되어 성능저하가 필연적이라는 것을 의미한다.
그렇기 때문에 `Mutex code block를 최대한 적은 빈도로, 최대한 간결한 코드로만 작성`해야 한다. (ch 7 Mutex 내용)


<br>
------
<br>

## 심상민

### 1. 스레드가 무엇이고, 사용자 수준 스레드와 커널 수준 스레드의 차이점이 무엇인가요?

- 스레드

  - 프로세스 내에서 실제로 작업을 수행하는 주체
  - 프로세스 내부에 있는 CPU 수행 단위
  - 프로세스가 할당받은 자원을 이용하는 실행의 단위
  - 프로세스 내 작업 단위

- 사용자 수준 스레드

  - 스레드를 관리하는 라이브러리로 인해 사용자 단에서 생성 및 관리되는 스레드
  - 물리적으로 정말 커널 밖에 있는 것이 아니라, 커널 내부에 있지만 커널의 통제관 안에 있지 않음
  - 커널에는 '커널 모드'와 '사용자 모드' 두 가지가 있고, 여기서 '사용자 모드'에서 동작하는 스레드

- 커널 수준 스레드

  - 커널 레벨에서 생성되는 스레드
  - 운영체제 시스템 내에서 생성되어 동작하는 스레드로, 커널이 직접 관리


<br>
------
<br>

## 김장윤

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


<br>
------
<br>

## 김현준

### 1. CPU burst 시간 근사하는 법
OS가 CPU burst time을 예측하기 위해서는 기존에 사용되었던 동일한 프로세스의 사용시간을 기반으로 예측하게 된다. 이때 사용되는 식은 아래와 같다.

* Burst time(nth process) = alpha * actual burst time (n-1)th process + (1-alpha) * estimated burst time(n-1)th process 

이외에도 멀티 레벨 큐 스케쥴링처럼 프로세스의 종류를 나눔으로써 버스트 시간을 근사할 수 있다.

<br>
------
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


<br>
------
<br>

## 이재하

<br>

### 1. Convoy Effect (호위 효과) 란?
- convoy effect란 여러 스레드가 서로 스케쥴링되는 환경에서, FCFS (First come first serviced)일 경우, 매우 올래 걸리는 프로세스기 할당될 경우, 다른 스레드들이 이러한 프로세스에 영향을 받아서 전체적인 시스템 utilization이 떨어지는 현상을 말한다.
- ![ConvoyEffect](https://images.velog.io/images/leeesangheee/post/be806447-d912-41a1-98f9-c5292202c3fc/4.png)
  - cf) FCFS 스케줄링이란?
    - 먼저 요청한 프로세스를 먼저 처리하는 방법
    - 비선점 스케줄링 (처리시간 도중 처리하던 프로세스를 멈추고 타 프로세스를 실행하지 않음)
    - EX) 피자를 먹고싶다면 차례대로 와서 줄을 서세요. 배가 얼마나 고프던, 피자를 얼마나 빨리 먹던 상관없이 선착순으로 피자를 드립니다.