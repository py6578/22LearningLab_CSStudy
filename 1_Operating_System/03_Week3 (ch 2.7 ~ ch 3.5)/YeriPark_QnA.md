1. 프로세스 상태의 5단계  
: New - Ready - Run - Waiting - Terminated  
	- Run 상태에서 Ready 상태로 바꾸는 스케쥴러는?  
	: Job Scheduler가 Ready Queue로 프로세스를 옮긴다

2. PCB란 무엇인가?  
: PCB(Process Control Block)이란 프로세스의 정보를 담는 블럭이다.  
  Process State, Program Counter, CPU register, CPU scheduling information, Memory-management information, I/O status information을 저장한다
	- PCB를 교체하는 것을 무엇이라 일컫는가?  
	: Context Switching
	
	
	
	[기타 꼬리질문]  
	- IPC Shared Memory는 어떤 오버헤드가 존재하는가?  
	  : Kernel을 통해서 메시지를 전달해야 하는 오버헤드가 존재하므로 Shared 메모리보다 느리다.
	  
	
