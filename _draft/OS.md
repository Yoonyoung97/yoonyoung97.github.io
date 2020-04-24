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



프로세서 스케쥴링

​	잡 큐[하드웨어] : 모든 프로세서가 존재

​	레디큐[메인메모리] : CPU에 할당해서 준비단계

​	디바이스 큐 : 입출력 디바이스 와 관련된 동작을 기다리는 입출력 레디큐에 있습니다.

​	ㄹ오텀 스케쥴러 / 숏텀 스케쥴러

​	롱텀 : 잡큐 => 레디큐

​	숏텀 : 레디큐 => CPU

​	