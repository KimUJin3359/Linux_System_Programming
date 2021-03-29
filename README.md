# Linux_System_Programming

### 용어사전
- 컴퓨터 시스템 : **범용 기능**을 수행하도록 만들어진 시스템
- 임베디드 시스템 : **전용 기능**을 수행하도록 만들어진 시스템
- OS : **범용적**으로 쓰이는 **시스템 제어 프로그램**
- Firmware : **특정 목적**을 가진 시스템 전용 **시스템 제어 프로그램**
- 안드로이드 포팅 전문가 : OS를 새로 개발하지 않고, 안드로이드 소스코드를 HW에 맞게 수정하여 동작되게끔 하는 전문가
- 포팅 : 소스코드를 다운받아 HW에 맞게 수정하는 작업
- 컨트롤러 : 저장장치(RAM 등)의 CPU 역할
- ECU : 자동차의 CPU 역할
- Load : 저장장치에서 메모리로 

### 컴퓨터 시스템
#### 컴퓨터 시스템 구성
- APP
- OS
- HW

#### 임베디드 시스템 구성
- APP
- OS
- HW : Firmware or OS 필요
- 맞춤형 전용 시스템이기에 범용 APP을 만들기 힘듦
![4](https://user-images.githubusercontent.com/50474972/112774649-42ba2180-9075-11eb-9510-2a8dcf2ace04.png)

#### 시스템의 이해
- APP : User App
- OS : Library, System Call, Kernel
- HW : CPU, Memory, NVM(비휘발성 메모리)

### 시스템 개발 트렌드
- OS
  - 모델 마다 OS를 새롭게 개발 했었음
    - 팬택
    - 모토롤라 코리아
    - 삼성 애니콜 OS 개발자
    - LG OS 개발자
  - Android의 인기
    - 더 이상 신규 OS 개발이 필요 없어짐
- 로봇 시장 현황
  - 국내 로봇 주력
    - 청소 로봇
    - 서비스 로봇
  - 로봇팔 시장은 국내 매우 약함
- Firmware
  - DRAM
    - 수명을 길게 만들 수 있음
    - Firmware에 따라 수명의 차이가 생김
    - DRAM 내부 많은 Chip들을 제어, 관리
    - 외부로부터 신호를 받으면 원하는 결과를 전달해줄 수 있도록하는 전체적인 관리 시스템
  - Display
    - 디스플레이 제어 시스템
    - 내부 상태 감지
    - 외부로부터 신호를 받으면 원하는 화면을 보여줄 수 있도록하는 내부장치 관리 시스템
  - 차량
    - 자동차를 제어하는 시스템
  - 인포테인먼트 시스템
    - 차량 상태 정보를 받고, 모니터링 및 편의 제공 시스템
  - 모든 시스템에서 Android 사용이 힘든 이유
    - Android가 무겁기 때문
    - 고성능 HW에서만 Android 사용 가능 
 
### 임베디드 시스템 제어 프로그램
#### Firmware
- 임베디드 산업에서 가장 큰 비중 차지
- 전체 개발(직접 구현)
- 쓰레드 등 모든 기능을 직접 구현해야함

#### RTOS(Real Time OS)
- 가벼운 Firmware
- 쓰레드가 필요할 때 사용
- 엄격한 **인증이 필요할 때** 사용
- 종류
  - VxWorks : 현대그룹 SW개발, 국방, 항공
  - FreeRTOS
    - AWS 소유

#### 리눅스 커널
- 편리한 App 개발
- 불편한 장치 제어
- App 개발 비중이 높을 때 사용

#### Android

### 시스템 구성요소
#### 컴퓨팅 시스템
- 폰노이만 구조
- 현대식 컴퓨터 원리
  - CPU, 메모리, 저장장치
    - 메모리가 없었을 당시, 저장장치가 명령어 한줄 씩 CPU에게 전달(저장장치의 속도로 인해 성능 저하)
    - 메모리(반도체)에 저장장치의 데이터를 받아와서 빠르게 CPU(반도체)에게 전달
    ![5](https://user-images.githubusercontent.com/50474972/112780274-7603ad00-9083-11eb-8436-f70096ed3ac5.PNG)
  - 캐시메모리
    - 메모리(DRAM)와 CPU사이의 속도를 더 빠르게 하기위하여, CPU 내부의 메모리(캐시메모리, SRAM)를 둠
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
- 임베디드 CPU(MCU : Micro Controller Unit)
  - SoC 설계

#### CPU 대표 회사
- PC : Intel, AMD
- Mobile(ARM Core 사용) : 퀄컴(SOC)
- MCU(임베디드, ARM Core 사용) : 마이크로칩스(SOC), ST 마이크로 일렉트로닉스(SOC), NXP(SOC)
- SoC 생산 : TSMC, 삼성
