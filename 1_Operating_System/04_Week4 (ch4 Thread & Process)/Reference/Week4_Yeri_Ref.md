# Ch3/4. Process & Thread 

<br>
<br>

## 박예리
### Longterm scheduler(Job Scheduler)와 Shortterm scheduler(CPU Scheduler)
![https://media.geeksforgeeks.org/wp-content/uploads/20191227161652/Untitled-Diagram-150.png](https://media.geeksforgeeks.org/wp-content/uploads/20191227161652/Untitled-Diagram-150.png)
- Long-Term Scheculer : Long-Term Scheduler takes the process from job pool. 
			Job Pool에서 Ready Queue에 올릴 프로세스 선정
- Long-Term Scheculer : Short-Term Scheduler takes the process from ready queue.

[Difference between Long-Term and Medium-Term Scheduler](https://www.geeksforgeeks.org/process-schedulers-in-operating-system/)
	
<br>
<br>

### Process Structure (by Jaeha)
![https://user-images.githubusercontent.com/23491962/98322577-1a307d00-202b-11eb-967d-bfb5da6aecea.JPG](https://user-images.githubusercontent.com/23491962/98322577-1a307d00-202b-11eb-967d-bfb5da6aecea.JPG)

- 프로세스는 위 그림과 같이
    - code
    - Data
    - Heap - 동적 메모리에 할당되는 부분이 여기에 존재한다.
    - Stack - 프로세스 안에 thread가 존재하는데, 각각의 thread는 고유의 stack 영역을 가진다.

<br>
<br>


## DOM (Degree of Multiprogramming)
Degree of multi-programming is concerned with the maximum number of processes  a single processor can accommodate efficiently . 

The long term scheduler is responsible for determining the degree of multi-programming in OS which  take newly created processes to keep in the ready queue. 
[link](https://cdnpractice.geeksforgeeks.org/problems/explain-degree-of-multiprogramming)
[link2](https://truemind5.blogspot.com/2017/05/16-1.html)

<br>

## Q. 왜 유저 스레드를 사용하면 안정성이 떨어지는지?
[커널 스레드를 사용하면 안정적이지만 유저 모드에서 커널 모드로 계속 바꿔줘야 하기 때문에 성능이 저하된다. 반대로 유저 스레드를 사용하면 안정성은 떨어지지만 성능이 저하되지는 않는다.](https://parksb.github.io/article/8.html)  
![https://o.quizlet.com/Uj0kEi8FsySdYxE5ZZ1LuA_b.png](https://o.quizlet.com/Uj0kEi8FsySdYxE5ZZ1LuA_b.png)  
- 여기서 말하는 안정성이란 무엇인가?  
	- Thread-safe : if it behaves correctly when used from multiple threads, regardless of how those threads are executed, and without demanding additional coordination from the calling code.   
			멀티 스레드 프로그래밍에서 일반적으로 어떤 함수나 변수, 혹은 객체가 여러 스레드로부터 동시에 접근이 이루어져도 프로그램의 실행에 문제가 없음을 뜻한다. [link](https://eun-jeong.tistory.com/21)  
		1) Mutual Exclusion : 공유 자원을 꼭 사용해야 하는 경우 자원의 접근을 세마포어 등의 lock으로 통제한다. 통상적으로 사용되는 방법이다.  
		2) Thread Local Storage : 각각의 스레드에서만 접근 가능한 저장소들을 사용함으로써 동시 접근을 막는다.  
		3) Re-entrancy : 어떤 함수가 한 스레드에 의해 호출되어 실행 중일 때, 다른 스레드가 그 함수를 호출하더라도 그 결과가 각각에게 바르게 주어져야 한다.  
		4) Atomic Operation : 공유 자원에 접근할 때 원자적으로 정의된 접근 방법을 사용한다.  
		5) Immutable Object 등의 방법이 제안된다.  
	
	
	- 사용자 수준 Thread와 커널 수준 Thread 의 차이  
		- Kernel level thread : 커널 스레드는 가장 가벼운 커널 스케쥴링 단위다   
					하나의 프로세스는 적어도 하나의 커널 스레드를 가지게 된다.  
					
					
					[장점]  
					커널이 직접 스레드를 제공해 주기 때문에 안정성과 다양한 기능이 제공.    
					프로세스의 스레드들을 몇몇 프로세서에 한꺼번에 디스패치 할 수 있기 때문에 멀티프로세서 환경에서 매우 빠르게 동작    
					
					
					[단점]  
					스케줄링과 동기화를 위해 커널을 호출하는데 무겁고 오래걸린다.(저장한 내용을 다시 불러오는 과정이 필요)  
					즉, 사용자 모드에서 커널 모드로의 전환이 빈번하게 이뤄져 성능 저하가 발생한다.  
  
  
  
		- User level Thread : 	커널에 의존적이지 않은 형태로 스레드의 기능을 제공하는 라이브러리를 활용하는 방식이 사용자 레벨(User Level) 스레드  


					[장점]  
					스케줄링 결정이나 동기화를 위해 커널을 호출하지 않기 때문에 인터럽트가 발생할 때 커널 레벨 스레드보다 오버헤드가 적다.  
					즉, 위의 말은 사용자 영역 스레드에서 행동을 하기에 OS Scheduler의 context switch가 없다(유저레벨 스레드 스케줄러를 이용)  
					커널은 사용자 레벨 스레드의 존재조차 모르기 때문에 모드 간의 전환이 없고 성능 이득이 발생한다  
					
					
					[단점]  
					시스템 전반에 걸친 스케줄링 우선순위를 지원하지 않는다. (무슨 스레드가 먼저 동작할 지 모른다.)    
					프로세스에 속한 스레드 중 I/O 작업등에 의해 하나라도 블록이 걸린다면 전체 스레드가 블록된다. 
					=> 이게 안정성 문제인듯?  
		

