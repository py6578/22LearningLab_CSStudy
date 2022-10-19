# JAEHALEE : Week2 QnA

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
