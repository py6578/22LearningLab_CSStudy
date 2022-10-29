###  " Multicore Programming에서 동시성 과 병령성이란?"
(https://bubble-dev.tistory.com/m/entry/OS-%EB%A9%80%ED%8B%B0%EC%8A%A4%EB%A0%88%EB%93%9C-%EA%B0%9C%EB%85%90-%EB%8F%99%EC%8B%9C%EC%84%B1-vs-%EB%B3%91%EB%A0%AC%EC%84%B1)
- 병렬성 (Parallelism)
    - 실제 코어가 여러ㅐ여서 여러 작업들을 동시에 처리하는것
    - Data Parallelism : GPU에서의 작업처럼 작업은 동일하나 데이터만 나누는 것
    - Task Parallelism : 작업 자체를 나누어서 처리하는 것

- 동시성 (Concurrency)
    - 실제 코어는 하나지만 하나의 코어가 여러 작업을 빠르게 번갈아가면서 수행하며 마치 동시에 수행되는 것처럼 보이게 하는것

