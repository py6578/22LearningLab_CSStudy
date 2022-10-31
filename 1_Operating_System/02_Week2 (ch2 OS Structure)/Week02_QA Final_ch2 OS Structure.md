# Ch2. OS Structure

<br>
<br>

## 김현준
### 1. 시스템 콜과 api의 차이?
시스템 콜은 OS의 서비스를 직접적으로 실행시키는 명령어.
API는 프로그래머가 직접적으로 시스템 콜을 쓰지 않고 프로그램을 디자인하기 위한 인터페이스
또한, 시스템 콜을 직접 건드려서 프로그래밍을 하면, 호환성 문제가 있지만 api 기반의 프로그래밍은 같은 api를 지원하는 어떤 시스템에서도 호환 가능!
<br>
### 2. 동적 링킹과 정적 링킹의 차이?
[링크](https://live-everyday.tistory.com/69)
<br>
## 김장윤
### 1. 파라미터 전달 방법?
address of block을 전달, 프로그램에서 pushed, stacked되서 전달되는 방식이 있다.
cpu 레지스터 단위로 파라미터를 전달할 수 있는가 혹은 메모리에 올려서(주소값 생김) 파라미터를 전달하는 가의 차이
<br>
### 2. 윈도우에서 policy와 mechanism이 밀접하도록 인코딩 되어있는 데, 밀접하다는 의미는?
윈도우에서는 따로 policy와 mechanism을 분히시키지 않고, how(mechanism)와 what(policy)이 연결됨.
<br>
## 이재인
### 1. 하드췌어와 유저 인터페이스간 계층적 접근?
[링크](https://www.javatpoint.com/layered-structure-of-operating-system)
<br>
### 2. 마이크로 커널과 커널 차이 및 종류
마리크로 커널은 최소한의 프로세스와 메모리 관리를 제공하며 서비스를 제공하는 대신 통신을 이용하여 만듬
