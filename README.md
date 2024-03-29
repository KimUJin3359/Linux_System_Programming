# Linux_System_Programming

### 목차
- [용어사전](https://github.com/KimUJin3359/Linux_System_Programming#%EC%9A%A9%EC%96%B4%EC%82%AC%EC%A0%84)
- [컴퓨터 시스템](https://github.com/KimUJin3359/Linux_System_Programming#%EC%BB%B4%ED%93%A8%ED%84%B0-%EC%8B%9C%EC%8A%A4%ED%85%9C)
- [임베디드 시스템 제어 프로그램](https://github.com/KimUJin3359/Linux_System_Programming#%EC%9E%84%EB%B2%A0%EB%94%94%EB%93%9C-%EC%8B%9C%EC%8A%A4%ED%85%9C-%EC%A0%9C%EC%96%B4-%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%A8)
- [시스템 구성요소](https://github.com/KimUJin3359/Linux_System_Programming#%EC%8B%9C%EC%8A%A4%ED%85%9C-%EA%B5%AC%EC%84%B1%EC%9A%94%EC%86%8C)
- [Low-level 파일 입출력](https://github.com/KimUJin3359/Linux_System_Programming#low-level-%ED%8C%8C%EC%9D%BC-%EC%9E%85%EC%B6%9C%EB%A0%A5)
- [Process](https://github.com/KimUJin3359/Linux_System_Programming#process)
- [Context Switch](https://github.com/KimUJin3359/Linux_System_Programming/blob/master/README.md#context-switch)
- [Process State](https://github.com/KimUJin3359/Linux_System_Programming/blob/master/README.md#process-state)
- [Virtual Memory](https://github.com/KimUJin3359/Linux_System_Programming/blob/master/README.md#process%EC%9D%98-%EA%B0%80%EC%83%81-%EB%A9%94%EB%AA%A8%EB%A6%AC)
- [Timer](https://github.com/KimUJin3359/Linux_System_Programming/blob/master/README.md#timer)
- [Signal](https://github.com/KimUJin3359/Linux_System_Programming/blob/master/README.md#signal)
- [IPC](https://github.com/KimUJin3359/Linux_System_Programming#ipc)
- [Thread Programming](https://github.com/KimUJin3359/Linux_System_Programming#thread-programming)
- [Thread 응용](https://github.com/KimUJin3359/Linux_System_Programming#thread-%EC%9D%91%EC%9A%A9)
- [Race Condition](https://github.com/KimUJin3359/Linux_System_Programming#race-condition)

---

### 용어사전
- **컴퓨터 시스템** : **범용 기능**을 수행하도록 만들어진 시스템
- **임베디드 시스템** : **전용 기능**을 수행하도록 만들어진 시스템
- **OS** : **범용적**으로 쓰이는 **시스템 제어 프로그램**
- **Firmware** : **특정 목적**을 가진 시스템 전용 **시스템 제어 프로그램**
- 안드로이드 포팅 전문가 : OS를 새로 개발하지 않고, 안드로이드 소스코드를 HW에 맞게 수정하여 동작되게끔 하는 전문가
- 포팅 : 소스코드를 다운받아 HW에 맞게 수정하는 작업
- **컨트롤러** : 저장장치(RAM 등)의 CPU 역할
- **ECU** : 자동차의 CPU 역할
- **Load** : 저장장치에서 메모리로 데이터를 옮기는 작업
- **System Call** : Kernel에서 App을 만들 때 지원하는 API
- Device Driver : 장치를 관리하기위한 소프트웨어
- **프로그램** : **명령어의 집합**
- **프로세서**: **프로그램을 실행하는 칩셋**
- **프로세스** : **실행된 프로그램**, 리눅스의 task
- 프로세스 세그먼트 : **Text, Data, Bss, Stack, Heap**
- Task : 스케쥴링을 하는 단위
- MMU : phyiscal memory를 **virtual memory로 변경**하는 역할
- Kernel Thread : Kerner Space에서 생성되는 프로세스
- **Context Switch** : 한 프로세스에서 다음 프로세스로 **작업을 변경하는 것** 
- **IPC** : 프로세스간의 데이터 교환 방식
- **PCB(Process Descriptor)** : 프로세스를 제어하기 위한 **정보를 저장하는 블록**
- **Virtual Memory** : 각 프로세스들에게 부여되는 가상의 메모리
- **Interrupt** : 실행 중인 프로그램을 잠시 멈추고, Interrupt에 따른 작업 수행을 하도록 하는 것
- **Interrupt Handler(ISR)** : 해당 interrupt의 처리 방법(함수)
- **Signal** : Thread, Process에 정보를 전달하는 Interrupt의 한 종류 
- Race Condition : Thread, Process의 타이밍에 따라 결과 값이 달라질 수 있는 상태
- Critical Section : Thread, Process가 동시에 접근해서는 안되는 곳

---

### 컴퓨터 시스템
#### 시스템의 이해
- APP : User App
- OS : Library, System Call, Kernel
- HW : CPU, Memory, NVM(비휘발성 메모리)

#### 임베디드 시스템
- **전용 기능**을 수행하도록 만들어진 시스템
- 임베디드 시스템
  - APP
  - OS
  - HW : Firmware or OS 필요
- 맞춤형 전용 시스템이기에 범용 APP을 만들기 힘듦
![4](https://user-images.githubusercontent.com/50474972/112774649-42ba2180-9075-11eb-9510-2a8dcf2ace04.png)

---

### 시스템 개발 트렌드
- OS
  - 모델 마다 OS를 새롭게 개발 했었음
    - 팬택
    - 모토롤라 코리아
    - 삼성 애니콜 OS 개발자
    - LG OS 개발자
  - Android의 인기
    - 더 이상 신규 OS 개발이 필요 없어짐
    - 안드로이드 포팅 전문가 : 안드로이드 소스코드를 HW에 맞게 수정하여 동작되게함
- 로봇
  - 국내 로봇 주력
    - 청소 로봇
    - 서비스 로봇
  - 로봇팔 시장은 국내 매우 약함
- Firmware
  - DRAM의 Firmware
    - 수명을 길게 만들 수 있음
    - Firmware에 따라 수명의 차이가 생김
    - DRAM 내부 많은 Chip들을 제어, 관리
    - 외부로부터 신호를 받으면 원하는 결과를 전달해줄 수 있도록하는 전체적인 관리 시스템
  - Display의 Firmware
    - 디스플레이 제어 시스템
    - 내부 상태 감지
    - 외부로부터 신호를 받으면 원하는 화면을 보여줄 수 있도록하는 내부장치 관리 시스템
  - 차량의 Firmware
    - 자동차를 제어하는 시스템
- 모든 시스템에서 Android 사용이 힘든 이유
  - Android가 무겁기 때문
  - 고성능 HW에서만 Android 사용 가능 
 
---

### 임베디드 시스템 제어 프로그램
#### Firmware
- 임베디드 산업에서 가장 큰 비중 차지
- 전체 개발(직접 구현)
- 쓰레드 등 **모든 기능을 직접 구현**해야함

#### RTOS(Real Time OS)
- **가벼운 Firmware**
- 쓰레드가 필요할 때 사용
- 엄격한 **인증이 필요할 때** 사용
- 종류
  - **VxWorks** : 현대그룹 SW개발, 국방, 항공
  - **FreeRTOS**
    - AWS 소유

#### 리눅스 커널
- **편리한 App 개발**
- 불편한 장치 제어
- App 개발 비중이 높을 때 사용

#### Android
- 컴퓨터나 다를 것이 없음

---

### 시스템 구성요소
#### 컴퓨팅 시스템
- 폰노이만 구조
- 현대식 컴퓨터 원리
  - CPU, 메모리, 저장장치
    - 메모리가 없었을 당시, **저장장치가 명령어 한줄 씩 CPU에게 전달(저장장치의 속도로 인해 성능 저하)**
    - **메모리(반도체)에 저장장치의 데이터를 받아**와서 빠르게 **CPU(반도체)에게 전달**
    ![5](https://user-images.githubusercontent.com/50474972/112780274-7603ad00-9083-11eb-8436-f70096ed3ac5.PNG)
  - 캐시메모리
    - 메모리(DRAM)와 CPU사이의 속도를 더 빠르게 하기위하여, **CPU 내부의 메모리(캐시메모리, SRAM)**를 둠
    - cache miss, hit 발생

#### CPU, 메모리, 저장장치
- CPU(PC) 점유율 : Intel, AMD
- 메모리 점유율
  - DRAM : 삼성, SK, MICRON
- 저장장치 
  - SSD 점유율 : 삼성
  - HDD 점유율 : WD, Seagate, Toshiba
  - 플래시 메모리 점유율 : 도시바

#### CPU
- PC CPU vs 모바일 CPU

 | | PC CPU | Mobile CPU |
 | --- | --- | --- |
 | 전력원 | 전봇대 전기 | 배터리 |
 | | 전력을 많이 끌어옴(최대한 스피드) | 전력 소모를 아낌(극한 스피드) |

- Mobile CPU : IP 설계 -> SoC설계 -> 제조 
  1) IP 설계 : 칩을 설계(ARM, Ndivia 소유)
  2) 회로 설계 : IP를 사용한  설계 
    - 라이센싱
    - SOC(System On Chip) : 검은색 플라스틱 칩
      - 하나의 칩안에 여러개의 칩(Core, 계산, 모뎀, ... 다수 많은 기능)을 넣음
  3) 제조 : 파운드리 업체
- **임베디드 CPU(MCU : Micro Controller Unit)**
  - SoC 설계

#### CPU 대표 회사
- PC : Intel, AMD
- Mobile(ARM Core 사용) : 퀄컴(SOC)
- MCU(임베디드, ARM Core 사용) : 마이크로칩스(SOC), ST 마이크로 일렉트로닉스(SOC), NXP(SOC)
- SoC 생산 : TSMC, 삼성

---

### Low Level 파일 입출력
#### 리눅스에서의 파일
- **파일, 디렉토리들, 장치들(마우스, 키보드, 메모리)**
- 파일의 종류
  - 레귤러 파일/ 디렉토리/ 링크
  - Device 파일
  - Socket/ Pipe(IPC)
 
#### 파일 System Call
- 리눅스 **App에서** 리눅스 **커널에 요청을 위해 만들어둔 함수**
- 즉, Kernel에서 App을 만들 때 지원하는 API
  - 커널의 도움없이, C 언어 표준함수들만으로 동작될 수 없는 함수
  - printf : 화면 장치에 글자가 출력되어야 함, 그래픽 카드를 제어하는 커널 도움 받음
  - scanf : 키보드 I/O 장치 동작이 되어야함, 커널 도움 받음
 
#### 파일처리 API
- C언어 표준 함수
  - fopen : 리눅스의 System call인 open 함수 호출
  - fscanf : 리눅스의 System call인 read 함수 호출
  - fprintf : 리눅스의 System call인 write 함수 호출

#### Low Level 파일처리 API
- open, read, write 등 파일 관련 System Call
- 중요한 이유
  - 개발된 **'디바이스 드라이버' 사용시 사용**
  - **Firmware는 하나의 작은 운영체제**이며, **포인터로 장치 제어** 가능
  - **리눅스 OS는 거대한 운영체제**이며, **디바이스 드라이버를 통해서만 장치 제어** 가능  

#### vi에서 man 확인
1) vim에 API 이름을 적는다 (open, write ...)
2) [page 숫자] + shift + k
  - 1 : Linux Shell Command
  - 2 : System Call
  - 3 : Linux Library

#### File Descriptor
- 프로세스가 **파일에 접근하려 할 때 부여되는 정수**

#### open() System Call
- int open(path, flag, mode)
- flag
  - 필수
    - O_RDONLY (읽기만)
    - O_WRONLY (쓰기만)
    - O_RDWR (읽기, 쓰기 둘 다)
  - 추가
    - O_CREAT (없을 시 생성)
    - O_APPEND (덧붙이기)
    - O_TRUNC (파일 내용 제거 후 사용)
- mode
  - write할 떄 파일 권한, 0xxx값
  - open할 때는 파일 권한을 적어주지 않아도 됨
- 유의사항
  - error가 잦음
  - 음수 값일 때는, Error를 뜻함

#### close() System Call
- int close(fd)
- file descriptor만 적어주면 됨

#### read() System Call
- ssize_t read(fd, buf, count)
- buf에 count크기로 파일을 읽어 옴
- return value : 읽기 성공한 사이즈
- 읽어오기전에 memset을 통해 buf 초기화
- 구조체 정보도 읽기 가능

#### write() System Call
- ssize_t write(fd, buf, count)
- buf에 있는 값을 count 크기로 파일에 씀
- 구조체 정보도 쓰기 가능

#### File Offset
- 저장장치에서 어디까지 읽었는지 **offset 값을 내부적으로 가지고 있음**
- read 수행 시, offset 값 이동
- lseek : 'whence' + 'offset'
  - 기준점에서 offset만큼 떨어져 있는 곳으로 파일 offset을 옮기는 시스템콜
  - off_t lssek(int fd, off_t offset, int whence)
    - off_t : 정수(long), 음수가능
    - offset : 떨어져있는 곳
    - whence : 기준
  - whence
    - SEEK_CUR : 현재위치에서 부터
    - SEEK_SET : 시작점에서 부터
    - SEEK_END : 끝지점에서 부터
 
#### Standard IO와 Low Level 함수 차이
- 표준 입출력(Standard IO, High Level)
  - fopen, fseek, fclose 등 존재
  - **사용하기 쉽고, 기능이 많음**
  - **개발속도가 빠름**
  - Low Level 명령어를 감싼 Wrapping한 함수
- Low Level 명령어
  - 쓰기 불편
  - open, write, lseek 등 존재
  - **임베디드에서 Device File을 다뤄야 하기 때문에 사용**

---

### Process
#### 프로세스 용어 정리
- **프로그램** : **명령어의 집합**
- **프로세서**: **프로그램을 실행하는 칩셋**
- **프로세스** : **실행된 프로그램**

#### 프로세스
- 리눅스를 부팅하면 **최초의 프로세스가 존재하고, 모두 복제되어 생성**
- **각 프로세스는  PID가 존재**
- 부모 프로세스와 자식 프로세스가 존재
  - 자식 프로세스는 부모의 PID 값을 알고있음(PPID)
  - 부모 프로세스는 자식의 PID를 알지 못함

#### 프로세스 구성
- 하나의 프로세스는 **text, data, bss, stack, heap의 세그먼트**로 구성
- text : 코드
- data : 초기화된 전역
- bss : 초기화되지 않은 전역
- stack : 정적 변수(지역변수, 매개변수)
- heap : 동적 변수
- 로드될 때 text, data는 복사되고, bss, heap, stack은 공간만 만들어 둠

#### 프로세스의 탄생
- 0번 Process : 처음 태어난 프로세스
  - swapper
    - 오랫동안 사용하지 않은 **메모리를 디스크로 저장하는 SWAP 역할**
    - SWAP코드에서 PID 0번을 자기자신에게 부여
    - **PID 1, 2 번 생성**
  - 커널 자체이므로 프로세스 리스트에서 생략
- 1번 Process(**init Process**) : **User Space의 조상 프로세스**
  - init 프로세스가 fork 후 exec를 수행하여 독립적인 자식들을 생성
  - 역할
    - File System 마운트
    - Daemon 수행
    - Run level에 맞게 Shell 수행
    - 사용자 Login 대기
    - Shell 띄우기
- 2번 Process(**kthreadd**) : **Kernel Space의 조상 프로세스**
  - Kernel Space 내 생성되는 프로세스를 Kernel Thread라고 함
  - Kernel Thread를 생성

#### 프로세스 생성 Systemcall
- 방법 1 : fork
- 방법 2 : fork + exec
- fork
  - 자식을 낳음
  - 부모의 **메모리 내용을 자식에게 똑같이 복사**
- exec
  - 현재 프로세스를 **새로운 프로세스로 변경**
  - system("") 함수와 다르게 동작
    - **system함수는 프로세스 수행 후 돌아옴**
    - **exec는 현재 프로세스가 해당 프로세스로 바뀌어**, 새로운 프로그램 동작이 시작됨
- execl
  - execl("경로", "인자들", ... , NULL)
    - 인자가 없는 경우 ""를 하나 넣어주어야 함
    - 마지막에 NULL을 넣어주어야 함
  - execl이 실패하면 기존의 함수 실행
  - execl이 성공하면 현재 프로세스가 바뀜
- pid_wait
  - pid_wait(status)
  - 자식 프로세스 중 아무거나 끝나기를 기다림
  - 정리완료된 자식 프로세스의 pid 리턴
- wait_pid
  - wait_pid(pid, 0, 0);
  - 특정 pid가 끝나길 

#### 임베디드 프로세스
- Firmware
  - **단일 프로세스**
  - 프로세스가 끝나면 기기가 정지
  - 멀티 테스킹, 멀티 프로세싱이 필요할때는 RTOS, Linux급을 선택 

#### PID 확인
1. **ps -ef**
  - -e 옵션 : 커널 프로세스를 제외한 모든 프로세스 출력
  - -f 옵션 : full format/ PID 등 모든 정보 출력
2. **top**
  - htop 
  - 스케쥴링하는 단위를 task라고 함
  - 리눅스에서 task는 process

#### gdb
- 리눅스의 디버깅 도구
  - 프로그램을 한줄 씩 실행할 수 있는 기능(Trace)
  - 실행중인 프로그램의 감시를 시작할 수 있는 기능(Attach)
  - 해당 프로세스가 사용하는 메모리를 복사 할 수 있는 기능(Dump)
    ```
    sudo gdb -pid '번호'
    # 현재 실행중인 프로세스를 Attach하여 메모리 정보를 읽을 수 있음
    (gdb) dump memory '파일저장경로' '시작 주소' '끝 주소'
    # 종료
    hd '파일'
    ```
    
---

### Context Switch
#### Process Scheduling
- 멀티 프로세스 환경에서 하나의 CPU에 여러 프로세스를 수행하는 방법을 제시
- 하나의 Core는 **여러개의 프로세스를 순환하면서 수행**
  - 특정 시간마다 번갈아가면서 수행
  - 대체로, RR로 동작하며 OS마다의 계산 공식에 의해 우선순위가 변경됨
- 프로세스 간 메모리는 독립적으로 운영
  - **Virtual Address와 Physical Address**가 존재
  - 각자의 가상 메모리 주소 영역을 갖음
- **IPC(Inter Process Communication)**
  - 어떤 프로그램이 다른 프로그램에게 **값을 전달**하고자 할 때 사용
  1) 프로세스끼리 공유하는 메모리를 사용
  2) 커널의 도움을 받아 대신 전달해주는 방법 사용

#### PCB(Process Control Block)
- 커널이 **프로세스를 제어하기 위한 정보를 저장하는 블록**
- **Process descriptor**라고도 불림
- 주어진 시간이 다하여 다음 프로세스를 수행해야할 때, register 값들을 저장
  - Program Counter Register가 정상적으로 보구되어 끊겼던 곳 부터 이어서 수행이 가능함
- 저장정보
  - 프로세스 상태, PID 등
  - 프로세스에 대한 다양한 정보들을 보관(register 값)

#### Context Switching
- **Process 끼리 전환**을 Context Switching이라 함
- Process
- 자주 발생한다면 동시에 수행되는 것처럼 보임
  - 사용성이 좋아짐
  - 레지스터 복원, 복구 횟수가 잦아짐
- 적절한 스케쥴링 정책이 필요

---

### Process State
- **Run Queue**
  - 우선순위 값에 따라 스케쥴러가 먼저 수행할 것을 결정 지을 수 있는 후보들이 존재하는 큐
  - Run Queue에서 탈출 : I/O 응답 대기하거나, 종료 신호 발생 시
- **Running state(R)**
  - Context Switching으로 선택된 하나의 프로세스만 수행
  - 나머지 프로세스들은 Runnable (Ready) 상태에 있음
- **Uninterruptible Sleep state(D)**
  - 깨울 수 없는 sleep
  - 특정한 system call 호출 시 발생하는 state
  - mkdir 사용 시 응답이 올 떄 까지 대기
- **Interruptible Sleep state(S)**
  - 일반적인 sleep
    - sleep system call 사용 시
    - I/O 처리 후 응답 대기
    - timer 사용 시
- **Stopped state(T)**
  - SIGSTOP signal 사용 시
    - ctrl + z
    - kill -SIGSTOP 'PID'
  - SIGCONT signal 사용 시 다시 동작
- **Zombie state(Z)**
  - 하나의 프로세스는 자식 프로세스를 생성 가능(fork system call)
  - 자식이 죽으면 부모가 자식의 Process Descriptor(PCB) 제거
  - 부모 프로세스와 자식 프로세스가 있을 때 자식 프로세스가 먼저 끝난 경우
    - 자식 프로세스의 Process Descriptor가 남아있음(Zombie state)
    - 부모에게 SIGCHLD Signal을 보냄
    - 부모 프로세스가 SIGCHLD를 받으면 wait system call을 호출하여 자식의 Process Descriptor 제거
![프로세스](https://user-images.githubusercontent.com/50474972/113254049-0ef32c00-9301-11eb-8b0c-29222da2f7de.png)

#### Zombie state
- fork
  - fork 수행 시, 자식 프로세스는 pid가 0으로 됨
  - 자식 프로세스를 갖는 부모 프로세스가 pid를 받음
  ```
  pid_t child_pid = fork();
  if (child_pid > 0)
    // 부모 프로세스
  else if (child_pid == 0)
    // 자식 프로세스
  ```

---

### Process의 가상 메모리
#### Virtual Memory
- **각 프로세스들에게 제공되는 용량**
  - 실제 물리적 메모리보다 **더 큰 사이즈의 메모리를 쓸 수 있게 함**
  - 동시에 모든 메모리를 사용하는 일이 없기에 **자주 안쓰는 메모리를 HDD에 임시적으로 저장**
  - 만약의 사태에 대비해, **하드디스크를 메모리처럼 쓰는 SWAP 영역을 잡아서 사용**
- 장점
  - 모든 프로세스는 메모리 Address를 0x0000 0000 부터 사용 가능
  - 다른 프로세스가 쓰는 메모리가 있더라도 **신경쓰지 않고, 메모리를 사용**

#### Physical Memory
- DIMM(마더보드 부착형) 형태의 DRAM

#### MMU
- **가상 메모리를 사용하기위한 주소 장치 제공**
- **virtual memory를 physical memory로 변환**
- MMU가 없다면
  - 임베디드 커널 포팅 불가
  - OS말고 Firmware를 구현해야 됨
 
#### Virtual Address Space
- 각 프로세스는 **연속적인 메모리 공간을 사용하고 있다고 착각**하도록 함
  - 실제 물리적 주소와 다름
- 장점
  - 메모리 파편화에대한 구현이 쉬워짐
  - 저장장치를 메모리인양 사용가능(swap 영역)

#### htop 사용
- 메모리 필드
  - RES : Process가 사용중인 Physical memory 사이즈
  - VIRT : Process가 사용중인 Virtual memory 사이즈
  - SHR : Process가 사용중인 Shared memory 사이즈

- 단축키
  - F5 : Tree로 보기
  - Shift + H : User Thread 보기
  - Shift + K : Kernel Thread 

---

### Timer
#### UTC
- 국제 표준 시간
- 1972년부터 시행
- UTC + offset으로 시간표시
- 한국(KST) : ofsset(9)

#### RTC(Real Time Clock)
- 전원이 없어도 시간을 계산 함
- 수은 건전지 사용

#### 리눅스
- date
  - 부팅시 RTC 정보를 받아 리눅스에서 시간정보 관리
  - 네트워크에 연결될 때, Time 서버에서 자동으로 시간을 업데이트
- hwclock
  - RTC HW 장치가 가지고 있는 시간 정보 값
  - 리눅스에서는 date와 RTC가 같지 않으면 sync를 맞춰줘야함
  - 인터넷 Time 서버에서 시간값 가져와 sync 맞추기
    - sudo apt install rdate
    - sudo rdate time.bora.net
    - sudo hwclock -s : 시스템 시간 기준 RTC 시간 변경
    - sudo hwclock -w : RTC 시간 기준 시스템 시간 변경

#### time system call
- time_t time(NULL) : 1970년 1월 1일 0시 0분 0초부터 현재까지 지난 초
- time_t type : 64bit unsigned int
- localtime system call을 사용하면, 보기편한 정보로 확인 가능
  - struct tm : 현재 시간을 나타내는 구조체
    - 초, 분, 시간, 일, 월, 년
  - localtime()
    - time_t -> tm으로 변경
  ```
  struct tm {
  int tm_sec;
  int tm_min;
  int tm_hour;
  int tm_mday;
  int tm_mon;
  int tm_year;
  int tm_wday;
  int tm_yday;
  int tm_isdst;
  };
  ```
  
#### clock system call
- clock_t clock() : CPU clock이 아닌, process clock
  - 현재 프로세스가 시작되고 얼마나 시간이 흘렀는지를 반환
- clock_t type : long
- CLOCKS_PER_SEC 매크로 : 1초당 시스템 clock이 올라가는 정도(Windows : 1000, Linux : 1000000)를 나타냄

#### gettimeofday system call
- int gettimeofday(struct timeval \*tv, struct timezone \*tz
  - time system call과 같이 1970년 1월 1일로부터 지난 초를 얻어옴
  - time system call과 다르게 us단위로 정밀한 현재 시간을 얻을 수 있음
  - timeval, timezone 변수를 만들어 넣으면 system call이 적절한 값을 채워줌
  ```
  struct timeval
  {
    time_t tv_sec;
    suseconds_t tv_usec;
  }
  ```
  
#### Latency 값 구하기
- Latency
  - 자극과 반응 시간
  - 신호 전달 후 Response 시간
  - 함수 호출 후 리턴까지 시간

---

### Signal 
#### Interrupt
- CPU가 동작하는 중 하던 일을 멈추고 **다른 작업**을 하도록 하는 것
- Interrupt 발생 시 예약된 함수(ISR)가 동작
- Interrupt Handler(ISR) : interrupt에 대한 처리 방법
  - Handler를 지정해주지 않으면, 커널 내부에서 Default 동작을 수행함
- 주의
  - 일반 코드가 중지될 수 있음
  - ISR과 일반 함수 모두 같은 전역변수를 사용하는 경우, 코드에 버그가 발생할 수 있음
  - 도중에 Interrupt가 발생하면 안되는 곳에는 Interrupt Disable 처리를 해야 함

#### Signal
- Thread, Process에게 정보를 전달하는 신호
- Linux에서는 최대 256개 신호까지 전달할 수 있음
  - signal 종류 : kill -l
- 단순한 정보를 보낼 때 사용
- Interrupt의 일종

#### Signal API
- signal('시그널 번호', '핸들러 이름');
- 시그널 번호는 매크로로 사용해도 됨(전부 등록되어 있음)

#### Nestted Interrupt
  - ARM
    - 인터럽트에 우선순위가 존재 ( 낮은번호가 우선순위가 더 높음 )
    - 우선순위가 높은 Interrupt 발생 시 : 진행하던 Interrupt를 멈추고, 다시 Interrupt로 진입
    - 우선순위가 같은 Interrupt 발생 시 : 진행하던 Interrupt를 끝내고, 이어서 Interrupt로 진행
  - Linux
    - 우선순위가 존재하지 않음
    - 인터럽트 동작 중 인터럽트 발생 시 Nested Interrupt

#### Interrupt Enable/Disable
- man 3 page
- sigset_t
  - block 할 signal 마스크
- sigfillset
  - sigset에 전부 masking
- sigemptyset
  - sigset의 masking을 전부 비움
- sigaddset/sigdelset
- sigprocmask
  - sigprocmask(int how, const old_kernel_sigset_t *set, old_kernel_sigset_t *oldset)
  - how
    - SIG_BLOCK : 기존에 블록된 시그널이 있다면 두 번째 인자는 set의 시그널을 추가
    - SIG_UNBLOCK : 기존의 블록된 시그널에서 set의 시그널을 제거
    - SIG_SETMASK : 기존의 블록된 시그널을 전부 제거시키고 새로운 set의 시그널을 블록
  - set : 설정할 시그널
  - oldeset : 이 전에 블록된 시그널들을 저장
 
---

### IPC
- **Inter Process Communication**
- 동기화 처리 필요
  - **공유 리소스**(파일)로 통신
  - Process끼리 Shared memory 사용
    - 두 프로세서가 한 파일을 맵핑
    - 한 곳에 값이 바뀌면 모두 내용이 바뀜
    - 공유하고 싶은 값이 있다면 맵핑한 Address에 값을 적으면 됨
- 동기화 처리 필요 없음
  - Process와 Process 직접적으로 전송
  - **Mail box, Socket, Pipe** 등 사용

#### mmap
- 프로세스와 파일의 특징
  - 프로세스마다 **VIrtual Address Space를 가짐**
    - 독립적인 메모리 공간을 가짐
    - **공유 리소스를 통한 값을 전달**해야함
  - **파일은 모든 프로세스가 접근 가능**(shared resource)
- mmap (man 2 mmap)
  - 가상 메모리에 매핑
  - void \*mmap(void \*addr, size_t length, int prot, int flags, int fd, off_t offset);
  - 맵핑 할 주소 지정(addr)
    - 직접 주소 지정
    - NULL : 자동 선택, 맵핑된 주소 반환받음
  - 권한 지정(prot) : PROT_READ, PROT_WRITE, PROT_EXEC, PROT_NONE
  - flags : MAP_SHARED ...
  - offset : Page 사이즈의 배수로 지정
  - 메모리 값을 수정 시
    - 파일 내용도 함께 수정됨

#### Embedded에서 활용
```
#define BASE_ADDR ' '

int fd = open("/dev/mem", O_RDWR | O_SYNC);
base_addr = mmap(0, LENGTH, PROT_READ | PROT_WRITE, MAP_SHARED, fd, BASE_ADDR);

GPIO0 = base_addr;
GPIO1 = base_addr + 0x4;
...

*GPIO0 = 0xABCD
```
- **컴파일러 최적화**
```
while (1)
{
  *p = 1;
  sleep(1);
  *p = 0;
}
위와 같은 코드를 실행하면, compiler에서 최적화하여
*p = 1로 바꿔줌
이를 방지하기 위해 volatile 사용

volatile unsigned int *p = (volatile unsigned int *)'주소값';
```
- **비트 연산(Bit masking)**
  - reset : 어떠한 비트를 0으로 만듬
    - & 연산자 사용
    ```
      001001
    & 110111
    --------
      000001
    ```
  - set : 어떠한 비트를 1로 만듬
    - | 연산자 사용
    ```
      001000
    | 000010
    --------
      001010
    ```
    
--- 

### Thread Programming
- **한 프로세스**에서 특정 함수를 동시에 동작 시키고 싶을 때 사용
  - Pthread 라이브러리 사용
  - gcc -lpthread 옵션 사용
- 쓰레드 메모리 사용
  - **bss, data, text는 같은 공간**을 사용
  - **stack, heap은 쓰레드마다 독립적인 공간**을 사용
  ```
  static 변수는 data, bss영역에 할당되기 때문에 쓰레드 끼리 공유 가능
  
  void run()
  {
      static int cnt = 0;
      printf("%d\n", cnt);
      cnt++;
  }
  
  # 동기화 문제가 발생하는 원인
    1. CPU-메모리 속도차이 
      - CPU는 값을 요청하고, 저장하는 명령만 memory에게 함
      - 메모리에 값을 저장하기 전에 다른 쓰레드에서 값을 변경
    2. 쓰레드 A, B가 있을 때
      - A가 print를 하고 있을 때(cnt++ 전)
      - B도 print하여 같은 값을 출력
  ```

#### Thread 특징
- **Thread의 ID를 따로 관리**
- Thread끼리 **우선순위**가 존재
- Thread끼리 사용할 수 있는 stack의 사이즈를 결정할 수 있음
- 리눅스에서는 Process 단위가 아닌 **Thread 단위 스케쥴링**
  - task : 스케쥴러의 단위를 뜻함
  - Kernel에서 쓰는 Thread와 User Thread 모두 스케쥴링
  ![프로세스(1)](https://user-images.githubusercontent.com/50474972/113382688-16780b00-93bd-11eb-95b2-e59842192d44.png)
- Thread Control Block 개념
  - PCB처럼 Thread 별 정보가 저장되어 있음
    - Thread id(tid)
    - Thread State
    - 레지스터 
  ![프로세스(2)](https://user-images.githubusercontent.com/50474972/113382702-209a0980-93bd-11eb-9c92-fe75b14cb4b6.png)



#### pthread_create
- pthread_create(thread id, 쓰레드 속성, 함수, 파라미터)
  - thread id : thread id가 저장될 변수 주소
  - 쓰레드 속성 : 쓰레드 설정 Null이 default
  - 함수 : 실행할 함수
  - 파라미터(void \*) : 함수에 인자 값을 전달해주고 싶을 때 사용
  ```
  int num = 32;
  pthread_create(&tid, NULL, function, &num);
  
  In function
  int num = *(int *)ptr;
  ```
  
#### pthread_join
- pthread_join(thread id, thread 리턴 값)
  - join을 해야 쓰레드가 종료 됨을 기다린 후, 메모리 해제
  - pthread_join을 하지 않으면, thread가 종료되어도 메모리 해제가 안됨
 
#### pthread_cancel
- pthread_cancel(thread id)
  - thread 동작을 중지

#### pthread_self
- pthread_t id 값을 얻을 수 있음
- pthread_t type : unsigned long int

#### mutex_lock
- 동시성 에러가 발생할 때 사용
```
pthread_mutex_t lock;
pthread_mutex_lock(&lock);
...
pthread_mutex_unlock(&lock);
```

#### Thread Library
- glibc : C 표준 Library
  - GNU C Library
  - 리눅스 system call을 wrapping
  - PC를 위한 구현
  - glibc 이름 : libc-2.31.so
- newlib : 임베디드를 위한 C 표준 Library
  - 경량으로 제작됨
  - Free RTOS, GNU GCC에 사용 됨
- nanolib : newlib보다 더 작은 C 표준 Library
  - GNU Gcc에 사용 됨
- NPTL : glibc에서 사용하는 Library
  - Native POSIX Thread Library
  - glibc의 pthread를 구현
  - 1 : 1 Thread Model을 사용
    - User Level Thread와 Kernel Level Thread가 1:1로 매핑
    - 병렬 Core 동작에 유리, System Call 발생 시 User Thread 동작 정지 없음

#### 임베디드에서 Thread
- Firmware : Thread 사용 불가
- RTOS : Thread 지원
- Linux : 병렬 프로세싱 Thread 지원은 함
- Android : 병렬 프로세싱 Thread 사용

#### Mutli Thread vs Multi Process

| | Multi Thread | Mutli Process |
| --- | --- | --- |
| Context Switching | 빠름 | 느림 |
| 통신 | 빠름 | 느림 |
| 메모리 | 공유 리소스 issue 발생 | 메모리가 독립적으로 보호됨 |

---

### Thread 응용
#### Queue
- Thread끼리 통신을 할 때 사용하는 큐
  - 큐에 접근할 때 동기화 필요
    - Linked List로 구현
  - 큐가 꽉 차는 경우, Block 발생
  - push, pop 사용 시 동기화

#### Pipeline
- 각 단계로 이동할 때 병목현상을 없애고자 Queue를 사용
- 전용 대기 큐가 존재하고, 처리하는 쓰레드가 존재

#### Manager / Worker
- Manager가 Worker에게 작업을 분배
  - Manager가 Worker에게 지시
  - Shell로 동작 구현

#### Thread Pool
- Thread 생성, 제거 비용을 줄이고자 미리 제작
- 특정 동작을 하는 Thread를 작업 지시 전까지 대기 시킴


---

### Race Condition
- **Race Condition** : Thread, Process의 **타이밍에 따라 결과 값이 달라질 수 있는 상태**
- **Critical Section** 
  - Thread, Process가 **동시에 접근해서는 안되는 곳**
  - HW 장치를 사용하는 곳, Shared Resource 등

#### 원하지 않는 결과값
```
void run()
{
  for (int i = 0; i < 10000; i++) cnt++;
}
- 4개의 쓰레드를 돌려도, 실제 cnt값은 40000이 나오지 않음
```
- Single Thread 동작 원리
  1) cnt 변수를 레지스터로 복사
  2) 복사해온 레지스터 값에 1을 더함
  3) 계산이 완료된 레지스터 값을 메모리 값에 업데이트
- Multiple Thread 오류상황
  1) Thread A, B 가 존재할 때 A가 먼저 cnt 변수를 레지스터로 복사
  2) 복사해온 레지스터 값에 1을 더함
  3) Thread B가 cnt 변수를 레지스터로 복사
  4) Thread A가 변화된 cnt 값을 메모리로 업데이트
- 해결방법
  1) 지연을 걸어줌 : 함수가 오래걸리면, sleep도 오래 걸어줘야 하기 때문에 유지보수 측면에서 좋지 않음
    - Thread의 장점이 줄어듬
  2) Synchronization

#### Thread/Process Synchronization
- Critical Section을 **동시에 수행하지 않도록 하기 위해 서로 협의**를 맞추는 것
- 둘이서 하나의 HW 자원을 쓰거나, 하나의 변수를 사용할 때 한명씩 돌아가면서 쓰기 위해 협의를 해야 함
- 동기화 알고리즘
  - **mutex** : thread 동기화
  - **semaphore** : process 동기화
  - spin lock
  - barrier

#### mutex_lock
- **mutex_lock을 얻은 쓰레드 만이 share resource 사용**
- pthread_mutex_init(&mutex, attr)
  - mutex 객체 초기화
  - attr에 NULL을 넣으면 기본 값으로 처리
- pthread_mutex_destroy(&mutex)
  - mutex 객체 제거
- pthread_mutex_lock(&mutex)
  - mutex lock을 요청하여 얻음
  - 얻을 수 있을 때 까지 block
- pthread_mutex_unlock(&mutex)
  - mutex lock을 반환

