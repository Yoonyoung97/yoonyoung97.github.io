OS



기본적으로 OS는 사용자 프로세스 시스템이 여러 구성요소에 서비스를 제공

OS는 사용자에서 도움 주는 프로그램을 제공

 1. User Interface

    CLI / GUI / Batch

 2. Program execution

    Error ; execution

​	3. I/O operations 

​		file 입출력 / 디바이스 

 4. File-system manipulation

    R/W  file & directories

    Create and Delete file & directories

    Search file & directories

    list file Information

    permission management

    

 5.  Communications

    통신은 Processes 들 간의 통신을 주로 이야기 한다 .

    프로세스와 프로세스의 통신 중엔 shared memory [Buffer]를 사용한다 .

    message passing은 적절한 포트를 통해서 직접 메세지를 전달 

    

 6. Error detections

     OS에서 시그널을 생성했을 때 

    사용자 모드에서 시그널 생성했을 떄 

	7. Resource allocation

    하드웨어 할당 

	8. Accounting

    사용자가 어떤 자원을 얼마만큼 사용하는지 트래킹

	9. Protection and security

    Protection  :: 접근 제어 

    ​						어떤 리소스를 사용자/어플리케이션이 접근제어 할 수 있는지

    Security ::  사용자에 대한 보안 [접근 허용]

![image-20200323133854588](C:\Users\USER\AppData\Roaming\Typora\typora-user-images\image-20200323133854588.png)





CLI :: Command Interpreter 

1. Shell에 구현
2. Kernel에 구현 / 독립된 프로그램으로 구현됨



System Calls

​	OS가 제공하는 프로그래밍 인터페이스 

​    상위레벨에서 API를 사용합니다.

​	![image-20200323141304441](C:\Users\USER\AppData\Roaming\Typora\typora-user-images\image-20200323141304441.png)

System call은 넘버링이 되어있다. ㅡ

API는 1:1 mapping이 아니라 

여러개의 System 콜을 사용할 수 있다.

커널에서 제공하는 여러 기능을 사용하고싶다고 API에 요청

인터럽터::

>  When a User Mode process invokes a System call, the CPU switches to Kernel Mode and starts the execution of a kernel function.

하드웨어에서 인터럽터 시그널을 받으면 하드웨어 번호를 가지고 실행을 시킨다. 

각각 Interrupt Vector 번호로 표현 되어있어 구분가능함

소프트웨어 쪽에서 오는 Interrupt는 128번

 



Systemcall Parameter Passing

Register

Buffer

Stack



<<<<<<< HEAD


=====================================

Processes 스케쥴링

프로세스란 실행하고있는 프로그램 

프로세스 통신은 공유 메모리 ,프로세스 간 직접적 메세지 통신

1.1 Process Concept

​	단 하나의 프로세서만 처리할 수 있는 것 : Batch System == Job

​	Time-shared systems : programs or tasks

​	프로세서라고 하면 실행되는 프로그램이다.

​	프로세스는 여러 파트로 구성이 됩니다.

​	실행 되어야 하는 프로그램 명령어 코드가 존재 함 : Text Section

​	명령어가 실행하기 위해선 위치를 가르키는 프로그램 카운터가 존재해야 한다. 하드웨어 / 소프트웨어 각각 존재

​	또한 스택엔 파라미터/리턴주소/로컬변수가 들어갑니다.

​	글로벌 변수를 지정하면 Data Section에 들어간다.

​	동적 할당메모리는 Heap 에 들어간다.

​	실행가능한 프로그램이 메모리의 로딩된 것 == 프로세서

​	프로세서 : 코드 + 데이터 영역 + 스택 영역 + 프로세서 제어에 필요한 Process context

​	프로그램 = 실행가능한 코드

​	프로세서 = 액티브한 메모리에 로딩된 프로그램

​	프로그램을 실행하는 것은 GUI / CLI 로 실행

​	프로그램은 여러개의 프로세서로 실행 가능함.

​	Stack : 파라미터, 반환 주소, 로컬 변수 , temporally data

​	Heap : 동적 할당 구역

​	Data Section : 전역변수

​	text Section : 명령어 셋이 존재함.

​	프로세서는 new state (생성됨) $$\rightarrow$$ ready(프로세서가 실행되기 위해 준비 큐에 존재하는 단계 ) $$\rightarrow$$ running(스케쥴러에 의해서 cpu에 실행되게 끔 바꿔줌 : 실행되고 있는 단계) $$\rightarrow$$ 인터럽터에 의해서 ready로 갈수 있음 or 인터럽터 때문에 입출력 대기 중이면 ready로 돌아감 $$\rightarrow$$ 실행 종료시 terminated

​	

Process Control Block(PCB : Task control block) 

프로세서가 현재 어떤 상태에 있는지 알 수 있는 정보를 가지고 있음

Program counter : 다음번 실행될 위치를 지정해줌

CPU registers : 프로세서와 관련된 레지스터 정보를 가지고 있음

기타 등등



Threads 

​	프로그램 카운터가 여러개 존재한다.

​	

1.2 Process Scheduling 

=======
프로세서 스케쥴링

​	잡 큐[하드웨어] : 모든 프로세서가 존재

​	레디큐[메인메모리] : CPU에 할당해서 준비단계

​	디바이스 큐 : 입출력 디바이스 와 관련된 동작을 기다리는 입출력 레디큐에 있습니다.

​	ㄹ오텀 스케쥴러 / 숏텀 스케쥴러

​	롱텀 : 잡큐 => 레디큐

​	숏텀 : 레디큐 => CPU

​	
>>>>>>> f7f4b3e69116e343b2d6f9f882ed2294510c26da
