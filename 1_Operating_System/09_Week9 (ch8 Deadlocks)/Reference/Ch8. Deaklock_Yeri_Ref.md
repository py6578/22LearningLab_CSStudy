# Ch 8. Deadlocks
<br>
## 박예리

## 1. Producer-Consumer Problem
 ![https://simsimjae.tistory.com/70](https://simsimjae.tistory.com/70)
 ![https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Ft1.daumcdn.net%2Fcfile%2Ftistory%2F99151B3359CB9FA536](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Ft1.daumcdn.net%2Fcfile%2Ftistory%2F99151B3359CB9FA536)

 1. 소비자가 if(count==0)을 실행하자마자 스케쥴링이 일어나서 생산자가 cpu사용권을 획득했다.

2.생산자는 아이템을 생산하고 공유변수인 count를1증가시킨후에 자고 있지도 않은 소비자를 깨운다.

3. 아무일도 일어나지 않은 상태로 다시 스케쥴링이 일어나서 소비자가 sleep()을 실행해서 잠에 든다.

4. 그리고 다시 스케쥴링이 일어나서 생산자 프로세스가 실행되면 생산자는 count값이 2부터 시작해서 계속 증가하게 된다.

5. 생산자는 버퍼가 꽉찰때까지 (N이 100이 될때까지) 계속 생산하다가 count == N을 만족해서 잠이든다.

6. 결국에는 생산자 소비자가 둘다 잠에 든다는 문제가 발생한다.


![https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbVkApY%2Fbtqw9NIOBKp%2FLiHeQ8VeBAlVfeJRmGXNf0%2Fimg.png](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbVkApY%2Fbtqw9NIOBKp%2FLiHeQ8VeBAlVfeJRmGXNf0%2Fimg.png)

<br>
<br>

## 2. Readers-Writers Problem
![https://mblogthumb-phinf.pstatic.net/MjAyMDAxMjhfODUg/MDAxNTgwMTM3MzA0MTM1.d_rfH9R-z_Rf0PHiEfxcgWHRcnbJ7Pa-8CiqJdAiQ34g.1uaxvSpY4fp-epIgMM126jm2-JQBmmT4hIMkgho-WJYg.PNG.hirit808/image.png?type=w800](https://mblogthumb-phinf.pstatic.net/MjAyMDAxMjhfODUg/MDAxNTgwMTM3MzA0MTM1.d_rfH9R-z_Rf0PHiEfxcgWHRcnbJ7Pa-8CiqJdAiQ34g.1uaxvSpY4fp-epIgMM126jm2-JQBmmT4hIMkgho-WJYg.PNG.hirit808/image.png?type=w800)

![https://slidesplayer.org/slide/15164779/92/images/21/First+Readers-Writers+Problem.jpg](https://slidesplayer.org/slide/15164779/92/images/21/First+Readers-Writers+Problem.jpg)

- 특징! read_count 조차 다수의 readers 끼리의 공유자원이므로, 이 또한 mutex로 보호해야 한다.


<br>
<br>

## 3.Solution for Dining Philosopher Problem with No starvation 
![https://velog.velcdn.com/images%2Fminseojo%2Fpost%2F5cb6568d-be51-42fa-b860-6f02172fbd02%2Fimage.png](https://velog.velcdn.com/images%2Fminseojo%2Fpost%2F5cb6568d-be51-42fa-b860-6f02172fbd02%2Fimage.png)
![문제 정의 링크](https://velog.io/@minseojo/%EC%9A%B4%EC%98%81%EC%B2%B4%EC%A0%9C-%EC%8B%9D%EC%82%AC%ED%95%98%EB%8A%94-%EC%B2%A0%ED%95%99%EC%9E%90-%EB%AC%B8%EC%A0%9C)

[식사하는 철학자 문제]
1. 일정 시간 생각을 한다.
2. 왼쪽 포크가 사용 가능해질 때까지 대기한다. 만약 사용 가능하다면 집어든다.
3. 오른쪽 포크가 사용 가능해질 때까지 대기한다. 만약 사용 가능하다면 집어든다.
4. 양쪽의 포크를 잡으면 일정 시간만큼 식사를 한다.
5. 오른쪽 포크를 내려놓는다.
6. 왼쪽 포크를 내려놓는다.
7. 다시 1번으로 돌아간다.
<br>
간단하게 생각해, 만약 모든 철학자들이 동시에 자신의 왼쪽 포크를 잡는다면, 모든 철학자들이 자기 오른쪽의 포크가 사용 가능해질 때까지 기다려야 한다. 그런데 모든 철학자들이 그러고 있다. 이 상태에서는 모든 철학자가 영원히 3번 상태에 머물러있어 아무것도 진행할 수가 없게 되는데, 이것이 교착(Deadlock)상태
<br>


초기 상태: 사람 5명, 젓가락 5개

실행 과정: 5명의 사람이 순차적으로 사용하지 않은 젓가락을 1개씩 집으면서 2개의 쌍을 맞춘다. 그리고 밥을 먹은 후 젓가락을 내려 놓는다. 이 과정을 무수히 빠르게 진행한다.

문제 발생 시점: 5명의 사람 모두 젓가락을 1개씩 집은 상황에서 젓가락 5개를 모두 사용했지만 5명 누구도 식사를 하지 못한다. 여기서 젓가락을 나눠주지도 못하므로 5명이 젓가락 1개씩 들고 하루 종일 밥만 구경하는 교착(Deadlock)상태에 걸려 무한히 대기한다. 이렇게 한번 교착상태에 빠진 철학자들은 계속 고뇌만 하다가 기아현상(Starvation)으로 굶어 죽는다.
<br>

![Lecture note for Dining Philosopher](http://web.eecs.utk.edu/~mbeck/classes/cs560/560/notes/Dphil/lecture.html)
There are 8 solutions for Dining Philosopher problem in above link!

### Solution #6 -- Preventing starvation
So, in order to prevent starvation you either need:
A guarantee from the thread system that threads will be unblocked from monitors and condition variables in the same order that they are blocked. In such a case, solution #4 will work fine, since a blocked philosopher will then be guaranteed to get a chopstick once it is released. Of course, this doesn't solve the problem that philosopher 4 gets to eat more than the rest, but it does prevent starvation.
To do it yourself. In other words, you must guarantee that no philosopher may starve. For example, suppose you maintain a queue of philosophers. When a philosopher is hungry, he/she gets put onto the tail of the queue. A philosopher may eat only if he/she is at the head of the queue, and if the chopsticks are free.
Solution #6  implements this. When a philosopher calls pickup(), if the queue is empty, the chopsticks are checked, and if they are in use, the philosopher is put on the queue. If they are not in use, the philosopher is allowed to eat, and pickup() returns. Note how this checking must be performed in a monitor. When putdown() is called, the chopsticks are released, and then test_queue() is called, which checks the head of the queue to see if the philosopher there can eat. If so, that philosopher is unblocked, and then he/she can eat.

Try the program out to see that it works. Moreover, note that there are times when a philosopher can call pickup() and the sticks can be available, but the philosopher blocks. This is because the queue isn't empty. Thus, the solution may not allow philosophers to eat as much as they would like, but it does prevent starvation. Think about ways that you could prevent starvation, but also allow less blocking time for philosophers.

 shows the output of dphil6 5. Note how the total block time here is much higher than dphil_4 and dphil_5. This is because a philosopher might block even though the chopsticks are free, because another philosopher is hungry and on the queue.

2100 Total blocktime:  4441 :   884   887   912   857   901

<br>
<br>


<br>
<br>

## 4.Zombie / Orphan process and its solutions 
![https://www.geeksforgeeks.org/zombie-processes-prevention/](https://www.geeksforgeeks.org/zombie-processes-prevention/)


![https://stackoverflow.com/questions/284325/how-to-make-child-process-die-after-parent-exits](https://stackoverflow.com/questions/284325/how-to-make-child-process-die-after-parent-exits)