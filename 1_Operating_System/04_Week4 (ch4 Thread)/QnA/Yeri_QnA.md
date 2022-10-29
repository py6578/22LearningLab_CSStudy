# Ch3/4. Process & Thread 

<br>
<br>

## 박예리
### 1. MultiProcessing과 Multithreading의 차이 (+ Multicore는?)
Multiprocessing은 하나의 Task마다 {Code, Data, Heap, Stack} 레이아웃의 프로세스를 할당하여 한 프로세스가 한 작업만을 수행하는 것이다.
이에 반해, Multithreading은 한 프로세스 내에서 여러개의 Task를 수행할 수 있도록 해당 프로세스의 {Code, Data, Heap}은 공유하면서 Stack 만을 개별로 가지면서 여러 작업을 동시에 수행하는 것이다.
Multicore는 하드웨어적인 접근으로 코어가 여러개 있는 것. 

CPU Scheduler가 한 코어에 한 프로세스를 할당한다.
Thread는 Process의 흐름.

    Q. Multicore에서 Multithreading이 더 중요해진 이유?
    TBD... 

    #### 1-1. CPU의 병렬처리와 GPU의 병렬처리는 어떻게 다른가?
    CPU의 병렬처리는 여러개의 코어에서 동시적으로 여러개의 일을 수행하는 Task 관점의 병렬처리이고,
    GPU는 한 Task의 데이터를 수백개의 코어에 분할하여 반복적인 작업을 통해 빠르게 병렬 연산하는 병렬 처리를 의미한다. (Data의 병렬성)
    따라서 GPU는 병렬 연산은 가능하다 Multiprocessing은 아니다. 




