# Ch 3. Process

<br>
<br>

## 김현준

<br>

### 1. MS-DOS와 UNIX의 차이점
MS-DOS
* 사용자 프로그램이 입출력 루틴에 접근해 디스크 드라이브(저장 장치) 직접 쓰기 가능 (사용자 프로그램에 문제가 생기면 전체 시스템에 문제 발생)
* interface와 functionality 분리 X

UNIX
* 커널과 시스템 프로그램으로 나뉘어 MS-DOS에서 생기는 문제 발생 X
* interface와 functionality 분리 O
* 하지만 구현과 유지보수가 쉽지 않다

`   
### 2. system boot 과정
* 우선 OS는 비휘발성 저장장치(ROM)에 저장되고
* bootstrap 프로그램이 커널을 찾은 뒤, memory에 적재하고 실행


<br>
<br>

## 이재하

### Q1. 프로세스 구조에 대해 설명하세요

![https://user-images.githubusercontent.com/23491962/98322577-1a307d00-202b-11eb-967d-bfb5da6aecea.JPG](https://user-images.githubusercontent.com/23491962/98322577-1a307d00-202b-11eb-967d-bfb5da6aecea.JPG)

- 프로세스는 위 그림과 같이
    - code
    - Data
    - Heap - 동적 메모리에 할당되는 부분이 여기에 존재한다.
    - Stack - 프로세스 안에 thread가 존재하는데, 각각의 thread는 고유의 stack 영역을 가진다.
    
    으로 이루어져 있다.
    

### Q2. IPC 통신 방법은 크게 2가지로 존재하는데, 이때 그 중 하나인 Using Message Passing 방법에서 사용하는 연산은 무엇인가

![https://blog.kakaocdn.net/dn/bDS16L/btq6cUgBhUP/ctoU6yixvYtxP6TDYgU4zK/img.png](https://blog.kakaocdn.net/dn/bDS16L/btq6cUgBhUP/ctoU6yixvYtxP6TDYgU4zK/img.png)

- 1) Send : 메시지를 전송함
- 2) Receive : 메세지를 받음

<br>
<br>

## 황정호


### 1. UNIX의 `fork()`+`exec()`와 WINDOWS의 `CreateProcess()`의 차이는?
- `fork()`에 의해 만들어진 자식 프로세스 (child process)는 부모 프로세스(parent process)의 주소 공간을 복사함. fork 이후 자식과 부모 두 프로세스는 함께 실행되다가, 자식 프로세스에서 `exec()` 시스템 콜을 사용해서 새로운 프로그램을 메모리에 깔아줌. 이때 부모 프로세스는 wait()을 선언하고, 자식 프로세스가 exit()를 사용할 때까지 기다림.
- `CreateProcess()`는 자식 프로세스가 생성될때 어떠한 프로그램을 실행할지 요구하기 위해 특정 주소 값을 명확하게 적어줌. 
  - https://m.blog.naver.com/PostView.naver?isHttpsRedirect=true&blogId=and_lamyland&logNo=221095965255


### 2. `JIT (just-in-time) 컴파일`과 `AOT (ahead-of-time) 컴파일`을 비교하시오.
- `JIT 컴파일러`는 프로그램 자체를 실행하는 동안 기계어를 생성하며, `AOT 컴파일러`는 프로그램이 실행되기 전에 기계어를 생성함.
- `JIT 컴파일러`는 실행 시점에 인터프리트 방식으로 기계어 코드를 생성하면서 그 코드를 캐싱하여 같은 함수가 여러 번 불릴때 매번 기계어 코드를 생성하는 것을 방지함. 
- `AOT 컴파일러`는  목표 시스템의 기계어와 무관하게 중간 언어 형태로 배포된 후 목표 시스템에서 인터프리터나 JIT 컴파일 등 기계어 번역을 통해 실행되는 중간 언어를 미리 목표 시스템에 맞는 기계어로 번역.


<br>
<br>

## 박예리

### 1. 프로세스 상태의 5단계  
: New - Ready - Run - Waiting - Terminated  
	- Run 상태에서 Ready 상태로 바꾸는 스케쥴러는?  
	: Job Scheduler가 Ready Queue로 프로세스를 옮긴다

### 2. PCB란 무엇인가?  
: PCB(Process Control Block)이란 프로세스의 정보를 담는 블럭이다.  
  Process State, Program Counter, CPU register, CPU scheduling information, Memory-management information, I/O status information을 저장한다
	- PCB를 교체하는 것을 무엇이라 일컫는가?  
	: Context Switching
	
	
### 	[기타 꼬리질문]  
	- IPC Shared Memory는 어떤 오버헤드가 존재하는가?  
	  : Kernel을 통해서 메시지를 전달해야 하는 오버헤드가 존재하므로 Shared 메모리보다 느리다.


<br>
<br>

## 심상민

### 1. '프로세스 간 통신 모델' 두 가지는? 각 방법들의 특징은 무엇인가요? 
- '공유 메모리'
	- 공유 메모리 영역을 구축할 대만 시스템 콜이 필요하므로 빠름. (커널 도움 필요 없음)
	- 프로세스들은 동시에 동일한 위치에 쓰지 않도록 책임져야함.
		
- '메시지 전달'
	- 시스템 콜을 사용하여 구현되므로 커널 간섭 등의 부가적인 시간 소비 작업이 필요하여 느림.
	- 충돌을 회피할 필요가 없어 적은 양의 데이터를 교환하는 데 유용함.
	- 분산 시스템에서 구현하기 쉬움.

------------

### 2. '좀비 프로세스'와 '고아 프로세스'가 무엇인가요?
- '좀비 프로세스'
	- 종료되었지만 부모 프로세스가 아직 wait() 호출을 하지 않은 프로세스
- '고아 프로세스'
	- 부모 프로세스가 wait()를 호출하는 대신 종료
	- UNIX는 고아 프로세스의 새로운 부모 프로세스로 init 프로세스를 지정함으로써 문제를 해결함