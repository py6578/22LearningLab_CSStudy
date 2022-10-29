# Ch 3

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


### 2. system boot 과정
* 우선 OS는 비휘발성 저장장치(ROM)에 저장되고
* bootstrap 프로그램이 커널을 찾은 뒤, memory에 적재하고 실행

