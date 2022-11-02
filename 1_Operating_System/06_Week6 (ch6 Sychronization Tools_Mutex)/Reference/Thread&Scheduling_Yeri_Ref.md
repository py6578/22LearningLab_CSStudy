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

### 5. A solution to the critical-section problem
  1. __*Mutual exclusion*__ : If process Pi is executing in its critical section, then __no other processes can be executing__ in their critical sections.  
  2. __*Progress*__ : If no process is executing in its critical section and some processes wish to enter their critical sections, then only __those processes that are not executing in their remainder sections__ can participate in __deciding which will enter its critical section next__, and this selection __cannot be postponed indefinitely__.
  3. __*Bounded waiting*__ : There exists `a bound, or limit, on the number of times` that __other processes are allowed to enter__ their critical sections after a process has made a request to enter its critical section and before that request is granted.