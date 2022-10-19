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

## 커널 스레드를 사용하면 안정적이지만 유저 모드에서 커널 모드로 계속 바꿔줘야 하기 때문에 성능이 저하된다. 반대로 유저 스레드를 사용하면 안정성은 떨어지지만 성능이 저하되지는 않는다.
## Q. 왜 유저 스레드를 사용하면 안정성이 떨어지는지?



