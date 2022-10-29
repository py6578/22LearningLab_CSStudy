# Ch3/4. Process & Thread 

<br>
<br>

## 김민정
### 1. Multi-Processor Scheduling의 종류 두개와, 그 중 Symmetric multiprocessing(SMP)의 두가지 전략은?
Asymmetric Multiprocessing(ASP)과 Symmetric Multiprocessing(SMP).

Asymetric Processing
하나의 코어만이 시스템 데이터 구조에 액세스한다. 주 프로세서가 전체 시스템을 통제하고 다른 프로세서들은 주인의 명령을 따르거나 또는 미리 정해진 일을 수행한다. master-slave 시스템의 형태로서 주 프로세서가 종속 프로세서들을 스케쥴하고 일을 할당. 이러한 ASP는 간단하여 데이터 공유의 필요성을 줄인다.

Symmetric Multiprocessing
각 프로세서가 self-scheduling 하는 방식. 스케쥴러는 각 프로세서에 대해 ready queue를 검사하고 실행할 스레드를 선택하도록 하여 스케쥴링을 진행한다. 프로세서가 메모리와 입출력 버스 및 데이터 path를 공유하며, 하나의 운영체제가 모든 프로세서를 관리.

SMP는 다음과 같은 두가지 전략을 가진다.
![2strategies](https://velog.velcdn.com/images%2Fwilko97%2Fpost%2Fb997bc24-aacd-4450-b862-19aea8e13ebc%2Fimage.png)
1. All threads may be in a common ready queue.
2. Each processor may have its own private queue of threads.

### 1. 두가지 전략의 장단점과 그중 더 널리 사용되는 전략은?
1번 전략: ready queue를 공유하게 되면 race condition이 생길 수 있다. 따라서 각각의 프로세서가 같은 스레드를 선택하거나, 스레드가 queue에서 없어지지 않도록 주의해야 한다. 이런 race condition에서 공통의 ready queue를 보호하기 위해서 locking을 사용하는게 좋다. 하지만 모든 큐에 대한 액세스가 locking이 필요할 것이므로, performance bottleneck이 생길 수 있다.
2번 전략(더 널리 사용): ready queue를 공유함으로써 생기는 성능 저하가 없다. 더 효율적인 cache memory 사용이 가능하다. 각각의 queue 사이즈가 달라 프로세서의 작업량이 다양한데, 이를 프로세서마다 비슷하게 맞춰주기 위해 balancing algorithm을 사용한다.