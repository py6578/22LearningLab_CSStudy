# Ch 8. Deadlocks
<br>
## 박예리

## Q1. Liveness failure 과 deadlock의 차이?

- Liveness failure는 N개의 스레드가 자원 할당 부족으로 인해 의미없는 일을 keep busy(waiting 하지 않다)하게 반복하는 비효율 상태이고,
- Deadlock은 N개의 스레드가 서로가 서로의 자원을 참고함으로써(circular) 자원을 얻지 못하고 waiting 상태에 빠져버린 상태.  
=> 따라서 둘이 동시에 일어날 순 없다.

+) deadlock의 해결책이 Liveness failure의 해결책이 동시에 될 수도 있으나 (해결책이 둘 다 가능하다는 이야기이지, 둘이 동시에 일어난다는 이야기는 아님), deadlock의 해결책이 무조건 liveness failure의 해결책인 것은 아님!



 ![https://www.geeksforgeeks.org/deadlock-starvation-and-livelock/](https://www.geeksforgeeks.org/deadlock-starvation-and-livelock/)

__Livelock(liveness failure)__ occurs when two or more processes continually __repeat the same interaction__ in response to changes in the other processes __without doing any useful work__. These processes are __not in the waiting state__, and they are running concurrently.  
This is different from a deadlock because in a deadlock __all processes are in the waiting state__. 

<br>
------
<br>