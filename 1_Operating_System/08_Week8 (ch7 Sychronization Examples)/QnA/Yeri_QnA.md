# Ch7. Sychronization Examples

<br>
<br>

## 박예리
### Q. Readers-Writers Problem이란 무엇이고 그 특징과 주의점은 무엇인가?
![https://mblogthumb-phinf.pstatic.net/MjAyMDAxMjhfODUg/MDAxNTgwMTM3MzA0MTM1.d_rfH9R-z_Rf0PHiEfxcgWHRcnbJ7Pa-8CiqJdAiQ34g.1uaxvSpY4fp-epIgMM126jm2-JQBmmT4hIMkgho-WJYg.PNG.hirit808/image.png?type=w800](https://mblogthumb-phinf.pstatic.net/MjAyMDAxMjhfODUg/MDAxNTgwMTM3MzA0MTM1.d_rfH9R-z_Rf0PHiEfxcgWHRcnbJ7Pa-8CiqJdAiQ34g.1uaxvSpY4fp-epIgMM126jm2-JQBmmT4hIMkgho-WJYg.PNG.hirit808/image.png?type=w800)

![https://slidesplayer.org/slide/15164779/92/images/21/First+Readers-Writers+Problem.jpg](https://slidesplayer.org/slide/15164779/92/images/21/First+Readers-Writers+Problem.jpg)

- 정의) Reader는 여러 Reader가 동시에 read가 가능하더라도, Write 할 때에는 데이터의 consistency를 위해서 해당 데이터의 접근에 대해 세마포어/뮤텍스로 접근권한을 보호해야한다.
    - 동시에 여러명의 Reader는 가능하나, Writer는 한 명만 가능하고 그 사이 Read 못하게 상호 배제
    - Shared_mutex를 통해 구현하기도 한다.
![https://i.stack.imgur.com/PStSm.jpg](https://i.stack.imgur.com/PStSm.jpg)

- 주의점) read_count조차 다수의 readers 끼리의 공유자원이므로, 이 또한 mutex로 보호해야 한다.

### Concurrent Programming Read / Write by Shared lock Example

```
#include <iostream>
#include <thread>
#include <chrono>
#include <mutex>
#include <shared_mutex> // C++17
#include <string_view>
using namespace std::literals;


// 1. 쓰는 동안, 다른 스레드는 읽을수 없어야 한다.
// 2. 쓰는 동안, 다른 스레드는 쓸수 없어야 한다.
// 3. 읽는 동안, 다른 스레드는 쓸수 없어야 한다.
// 
// 4. 읽는 동안, 다른 스레드도 읽을수 있어야 한다. <<=== 핵심 !!


// shared_mutex 동작 방식

// m.lock() 하면 : 다른 스레드의 m.lock(), m.lock_shared() 모두 대기 
//              => 쓰는 동안은, "쓰기, 읽기" 모두 금지
// 
// m.lock_shared() 하면 : 다른 스레드는 m.lock()은 대기
//                       다른 스레드의 m.lock_shared()는 대기 안함
//              => 읽는 동안에, "쓰기는 금지, 읽기는 가능"
// 
// Write  : m.lock(),        m.unlock()
// Reader : m.lock_shared(), m.unlock_shared(), 




//std::mutex m;

std::shared_mutex m;

int share_data = 0;


void Writer()
{
    while (1)
    {
        m.lock();
        share_data = share_data + 1;
        std::cout << "Writer : " << share_data << std::endl;
        std::this_thread::sleep_for(1s);
        m.unlock();
        std::this_thread::sleep_for(10ms);
    }
}


void Reader(const std::string& name)
{
    while (1)
    {
        m.lock_shared();
        
        std::cout << "Reader(" << name << ") : " << share_data << std::endl;
        std::this_thread::sleep_for(500ms);
        m.unlock_shared();

        std::this_thread::sleep_for(10ms);
    }
}

int main()
{
    std::thread t1(Writer);
    std::thread t2(Reader, "A");
    std::thread t3(Reader, "B");
    std::thread t4(Reader, "C");
    t1.join();
    t2.join();
    t3.join();
    t4.join();
}
```