# Ch5/4. CPU Scheduling & Thread 

<br>
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



