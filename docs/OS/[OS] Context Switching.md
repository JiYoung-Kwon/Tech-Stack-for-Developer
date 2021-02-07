# [OS] Context Switching

:writing_hand: *Assembled by JiYoung-Kwon (2021-01-19)* 



## 1. Context란?

* 사용자와 다른 사용자, 사용자와 시스템 또는 디바이스간의 상호작용에 영향을 미치는 사람, 장소, 개체등의 현재 상황(상태)을 규정하는 정보들
* OS에서는 CPU가 해당 프로세스를 실행하기 위한 해당 프로세스의 정보들을 말함
* Context는 프로세스의 PCB(Process Control Block)에 저장됨
  * PCB
    * 운영체제의 커널 내부에 존재
    * 각 프로세스의 생성과 동시에 생성
    * 프로세스 종료 시 함께 사라짐
    
  * PCB 저장정보
    
    ![img](https://media.vlpt.us/images/sohi_5/post/c54829db-134a-479c-b1ec-ac97174db1a6/image.png)
    
    * 프로세스 식별자(Process ID)
    * 프로세스 상태(Process State) : 생성(create), 준비(ready), 실행(running), 대기(waiting), 완료(terminated)
    * 프로그램 카운터(Program Counter) : 프로세스가 다음 실행할 명령어 주소
    * 사용 중인 레지스터 정보
    * CPU 스케줄링 정보 : 우선순위, 최종 실행시각, CPU 점유시간 등
    * 메모리 관리 정보(Memory limits)
    * 입출력 상태 정보 : 프로세스에 할당된 입출력 장치 목록, 사용 파일 목록 등
    * 포인터 : 부모,자식 프로세스에 대한 포인터, 프로세스가 위치한 메모리 주소에 대한 포인터, 할당된 자원에 대한 포인터 정보

<br/>

## 2. Context Switching이란?

* CPU가 실행하는 프로세스가 교체되며 CPU에서 관리하는 Context가 교체되는 것
* 멀티프로세스 환경에서 CPU가 어떤 하나의 프로세스를 실행하고 있는 상태에서 <u>인터럽트 요청에 의해 다음 우선 순위의 프로세스가 실행되어야 할 때</u>, 기존의 프로세스의 상태 또는 레지스터 값(Context)을 저장하고 CPU가 다음 프로세스를 수행하도록 <u>새로운 프로세스의 상태 또는 레지스터 값(Context)</u>를 **교체하는 작업**
* 컨텍스트 스위칭을 통해 멀티프로세싱, 멀티스레딩을 구현할 수 있음
* CPU 개수와 스레드 개수가 같으면 Context Switching이 발생할 일이 없음
  * 실행 중(Runnable) 상태의 스레드가 CPU 개수보다 적을 경우 문제 X
* 기계어 명령어 단위로 이루어짐
* 프로세스 간의 Context Switching은 OS 스케쥴러가 담당
* Context Switching를 하는 동안 **해당 CPU는 아무런 일을 하지 못함**
  * 잦은 컨텍스트 스위칭은 오버헤드를 발생시켜 CPU의 성능을 저하시킬 수 있음

#### 2-1. Context Switching - 인터럽트(Interrupt)

* 인터럽트 : CPU가 프로그램을 실행하고 있을 때 실행 중인 프로그램 밖에서 예외 상황이 발생하여 처리가 필요한 경우, CPU에게 알려 예외 상황을 처리할 수 있도록 하는 것

* Context Switching이 일어나는 인터럽트 경우
  1. I/O request (입출력 요청 시)
  2. time slice expired (CPU 사용시간 만료 시)
  3. fork a child (자식 프로세스를 만들 때)
  4. wait for an interrupt (인터럽트 처리를 기다릴 때)

<img src=./resources/context_switching.png width = 90%>

<br/>

## :page_with_curl: Reference

[[운영체제] Context Switching](https://velog.io/@sohi_5/%EC%9A%B4%EC%98%81%EC%B2%B4%EC%A0%9C-Context-Switching-suaduxev)

[OS - Context Switch(컨텍스트 스위치)가 무엇인가?](https://jeong-pro.tistory.com/93)

[OS :: 컨텍스트 스위칭 (Context Switching)](https://m.blog.naver.com/PostView.nhn?blogId=rhkdals1206&logNo=221575121342&proxyReferer=https:%2F%2Fwww.google.com%2F)

[컨택스트 스위칭(Context Switching) 개념정리](https://pearlluck.tistory.com/m/150?category=830586)