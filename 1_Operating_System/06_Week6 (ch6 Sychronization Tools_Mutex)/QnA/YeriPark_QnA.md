# Ch5/6. CPU Scheduling & Synchronization Tools

<br>
<br>

## 박예리
### 1. Mutex를 빈번하게 사용하면 코드의 성능 저하를 일으킨다는 것이 무슨 의미인가?

:Mutex를 사용하게 되면 그 critical section 내에서는 컨텍스트 스위칭이 일어나지 않고, 그 전 후에서도 오류를 방지하기 위해 시스템 단위에서 interrupt call을 일으키지 않는다. 때문에 mutex를 빈번히 사용(lock/unlock)한다는 것은 멀티스레딩(멀티프로세싱)이 자원을 효율적으로 스케쥴링해서 사용하는 것이 아니라 정지/대기 상태를 유도하기 때문에 실행시간의 성능저하를 유도할 수밖에 없다.  
