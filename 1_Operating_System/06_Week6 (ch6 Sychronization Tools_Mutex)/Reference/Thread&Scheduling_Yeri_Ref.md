# Ch6. Sychronizing Tools - Mutex
<br>
## 박예리

### 1. Race Condition
: where several processes access and manipulate __the same data concurrently__ and the outcome of the execution depends on __the particular order__ in which the access takes place  
Sol) we need to ensure that __only one process__ at a time can be manipulating the variable count

### 2. Q) prominence of multicore systems has brought an increased emphasis on developing multithreaded applications
: TBD 찾아보기

### 3. critical section
: the process may be accessing — and updating — data that is shared with at least one other process.
- to synchronize their activity so as to cooperatively share data.

### 4. General structure of a typical process
![http://www.expertsmind.com/CMSImages/667_l%20structure%20of%20a%20typical%20process.png](http://www.expertsmind.com/CMSImages/667_l%20structure%20of%20a%20typical%20process.png)

- entry section: The section of code implementing this request  
- exit section  
- remainder section : The remaining code 

### 5. Solutions to the critical-section problem
  1. __*Mutual exclusion*__ : If process Pi is executing in its critical section, then __no other processes can be executing__ in their critical sections.  
  2. __*Progress*__ : If no process is executing in its critical section and some processes wish to enter their critical sections, then only __those processes that are not executing in their remainder sections__ can participate in __deciding which will enter its critical section next__, and this selection __cannot be postponed indefinitely__.
  3. __*Bounded waiting*__ : There exists `a bound, or limit, on the number of times` that __other processes are allowed to enter__ their critical sections after a process has made a request to enter its critical section and before that request is granted

### 6. to handle critical sections in operating systems: preemptive kernels and nonpreemptive kernels. 
 - __*preemptive kernel*__ : allows a process to be preempted while it is running in kernel mode.
  - Advantage
    - A preemptive kernel may be more responsive, since there is less risk that a kernel-mode process will run for an arbitrarily long period before relinquishing the processor to waiting processes
    - a preemptive kernel is more suitable for real-time programming, as it will allow a real-time process to preempt a process currently running in the kernel.

 - __*nonpreemptive kernel*__ : does not allow a process running in kernel mode to be preempted
                              - a kernel-mode process will run until it exits kernel mode, blocks, or voluntarily yields control of the CPU


### 7. SMP(symmetric multiprogramming)
: (symmetric multiprocessing) is computer processing done by multiple processors that share a common operating system (OS) and memory [link](https://www.techtarget.com/searchdatacenter/definition/SMP)  
![https://cdn.ttgtmedia.com/rms/onlineimages/how_smp_shares_memory_space_with_different_processors-f.png](https://cdn.ttgtmedia.com/rms/onlineimages/how_smp_shares_memory_space_with_different_processors-f.png)
- In symmetric multiprocessing, `the processors share the same input/output (I/O) bus or data path`. A single copy of the OS is in charge of all the processors.
- SMP systems are better suited for online transaction processing than massively parallel processing (MPP) systems in which `many users access the same database` in a relatively simple set of transactions. 
Unlike MPP systems, SMP systems `can dynamically balance the workload` among computers to serve more users faster.
- The processors `__equally__ share main memory and have access` to all I/O devices.

##### SMP Advantages
- Increased throughput. : Using multiple processors to run tasks decreases the time it takes for the tasks to execute.
- Reliability. : If a processor fails, the whole system does not fail. But efficiency may still be affected.
- Cost-effective. : SMP is a less expensive way long term to increase system throughput than a single processor system, as the processors in an SMP system share data storage, power supplies and other resources.
- Performance. :Because of the increased throughput, the performance of an SMP computer system is significantly higher than a system with only one processor.
- Programming and executing code. : A program can run on any processor in the SMP system and `reach about the same level of performance`, which makes programming and executing code relatively straightforward.
- Multiple processors. : If a task is taking too long to complete, multiple processors can be added to speed up the process.


##### SMP Disadvantages
- Memory expense.: Because all processors in SMP share common memory, `main memory must be large enough` to support all the included processors.
- Compatibility. : For SMP to work, the OS, programs and applications all need to support the architecture.
- Complicated OS. : `The OS manages all the processors` in an SMP system. This means the design and management of the OS can be `complex`, as the OS needs to handle all the available processors, while operating in `resource-intensive` computing environments.

## SW based Solution to the Critical section problem
### 1. Peterson's Solution

## SW based Solution to the Critical section problem
### 1. Atomic
- Definition of atomic : one uninterruptible unit
![https://images.app.goo.gl/LR7Xh9taEfv285SX7](https://images.app.goo.gl/LR7Xh9taEfv285SX7)
- Usage
  - ensure mutual exclusion in situations where there may be a data race on a `single variable while it is being updated, as when a counter is incremented`
  - `special atomic data types` as well as `functions` for accessing and manipulating atomic variables
  - Disadvatages
      - they `do not entirely solve race conditions in all circumstances` 
      : Sec 6.1 의 `bounded-buffer problem`
        - the producer and consumer processes also have while loops whose condition depends on the value of count.
      - although their use is often limited to single updates of shared data such as counters and sequence generators

### 2. Mutex
![https://www.cs.uic.edu/~jbell/CourseNotes/OperatingSystems/images/Chapter5/5_01_CriticalSection.jpg](https://www.cs.uic.edu/~jbell/CourseNotes/OperatingSystems/images/Chapter5/5_01_CriticalSection.jpg)
<br>
  #### LOCK CONTENTION
  - Contend Lock : if a `thread blocks` while trying to acquire the lock  

    - high contention : a relatively large number of threads attempting to acquire the lock
                      -> decrease overall performance of concurrent applications
    - low contention : a relatively small number of threads attempting to acquire the lock

  - Uncontended Lock : If a `lock is available` when a thread attempts to acquire it

  #### DISADVANTAGES
  1. Busy waiting : 이미 한 프로세스가 critical section 안에 있을 때, 다른 프로세스가 mutex를 얻기 위해서 그 loop안에서 계속 대기 (continuously waiting)
    - Busy waiting 또한 CPU를 잡아먹는다
      - SOL) waiting 상태의 프로세스를 sleep 상태에 두고, mutex_lock이 사용가능할 때 깨운다

### 3. Spinlock
: when the lock is to be held for a short duration.
  the process spinswhile waiting for the lock to become available
  - ref [this link](https://brownbears.tistory.com/45)
: `Lock을 얻을 수 없다면, 계속해서 loop를 돌면서 Lock을 확인하며 얻을 때까지 재시도`한다. 이른바 바쁘게 기다리는 `busy wating`이다.
바쁘게 기다린다는 것은 `무한 루프를 돌면서 최대한 다른 스레드에게 CPU를 양보하지 않는 것`이다.

임계구역 진입을 위한 `대기 시간이 짧을 때 사용`하는게 바람직
  - Spin Lock을 사용하기 위한 `기준 대기 시간`?
    : lock을 얻는 데에 필요한 `두 번의 context switching 보다는 짧아야` 한다
      (1st : store to wait, 2nd : restore to make avaliable state from waiting state)

- Advantage
    1) Lock이 곧 사용가능해질 경우 컨택스트 스위치를 줄여 CPU의 부담을 덜어준다.
    : 운영 체제의 스케줄링 지원을 받지 않기 때문에 Context Switching이 일어나지 않는다.
    
- Disadvantage
    1) 스핀락을 `잘못 사용하면 CPU 사용률 100%를 만드는 상황`이 발생하므로 주의 해야 한다.  
    : 스핀락은 기본적으로 무한 for 루프를 돌면서 lock을 기다리므로 하나의 쓰레드가 lock을 오랫동안 가지고 있다면, 다른 blocking된 쓰레드는 busy waiting을 하므로 CPU를 쓸데없이 낭비
    2) 하나의 CPU나 하나의 코어만 있는 경우에는 유용하지 않다. 
    : 그 이유는 만약 다른 스레드가 Lock을 가지고 있고 그 스레드가 Lock을 풀어 주려면 싱글 CPU 시스템에서는 어차피 컨택스트 스위치가 일어나야 하기 때문

