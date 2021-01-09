# [NETWORK] OSI 7계층

:writing_hand: *Assembled by JiYoung-Kwon (2021-01-10)* 



#### :pushpin: OSI 7계층의 탄생

* 국제 표준 기구인 ISO(International Organization for Standardization)으로부터 탄생
* 처음 네트워크 장치 -> 회사의 장비마다 **호환**이 되지 않으며 복잡했음
* **호환성의 결여를 막기 위해** 네트워크를 7계층으로 분리하면서 표준을 만들게 되었음

***



## 1. OSI 7계층이란?

* OSI (Open Systems Interconnection Reference Model)
* 국제 표준화 기구(ISO)가 발표한 네트워크에서 통신이 일어나는 과정을 7단계로 나눈 것
* 통신 구조의 모델과 프로토콜의 표준 뼈대를 제공하기 위해 개발

![img](http://www.hellot.net/_UPLOAD_FILES/magazine/contents/Cap%202014-01-29%2010-08-23-964_1.jpg)

- Encapsulation
  - 응용 계층에서부터 데이터에 각각 헤더가 붙어 물리 계층까지 한단계씩 넘겨준다.
  - 최종적으로는 이진 비트가 전송된다.
- Decapsulation
  - 수신자가 받은 데이터를 다시 물리 계층 부터 헤더의 정보를 확인하고 떼어내는 과정을 응용 계층까지 반복한다.

## 2. OSI 7계층을 나눈 이유

* 통신이 일어나는 과정을 단계별로 파악할 수 있기 때문
* 흐름을 한 눈에 알아보기 쉽고, 사람들이 이해하기 쉬움
* 여러 회사 장비를 사용해도 네트워크에 이상이 없음
* 7단계 중 특정 부분에 이상이 생기면, 다른 단계의 장비 및 소프트웨어를 건들이지 않고도 이상이 생긴 단계만 고칠 수 있음



## 3. OSI 7계층 단계

* 상위 계층과 하위 계층으로 나뉨
  * 상위 : 7, 6, 5
  * 하위 : 4, 3, 2, 1

#### 7 계층 - Application Layer (응용 계층)

* 사용자와 가장 가까운 계층 (최상위)

* 사용자 인터페이스의 역할을 담당

* 응용 프로세스와 직접 관계하여 일반적인 **응용 서비스를 수행**

  * 네트워크 소프트웨어 UI 부분, 사용자 입출력(I/O) 부분

* 프로토콜 종류 

  > HTTP, SMTP, DNS, POP3, FTP, IMAP, Telnet 등...

#### 6 계층 - Presentation Layer (표현 계층)

* 데이터를 어떻게 표현할 지 정하는 역할을 하는 계층 (데이터 Format 결정)

* 코드 간 번역 담당. MIME 인코딩, 암호화 등...

  * 사용자의 명령어를 완성 및 결과 표현. 포장/압축/암호화

* 프로토콜 종류

  > ASCII, EBCDIC, CIF, JPEG, AVI, MPEG 등...

#### 5 계층 - Session Layer (세션 계층)

* 응용프로그램들 간의 통신을 관리하기 위한 방법 제공

* 세션 설정, 유지, 종료, 전송 중단 시 복구 등...

* 프로토콜 종류

  > SSH, TLS, NetBIOS 등...

#### 4 계층 - Transport Layer (전송 계층)

* 데이터 전송에 관한 서비스 제공

* 송/수신 측의 실질적인 연결을 설정하고 신뢰성 있는 통신이 가능하도록 함

* 사용하는 데이터 단위 : 세그먼트(segment)

* 데이터 전송을 위해 Port 번호 사용

* 프로토콜 종류

  > TCP, UDP 등...

#### 3 계층 - Network Layer (네트워크 계층)

* 목적지까지 가장 안전하고 빠르게 데이터를 보내는 기능. 최적의 경로 설정 (라우팅)

* 경로를 선택하고 패킷을 전달해주는 역할

* 데이터 단위 : 패킷(Packet)

* 대표적인 장비 : 라우터

* 프로토콜 종류

  > IP, ICMP, RIP, ARP 등...

#### 2 계층 - Data Link Layer (데이터 링크 계층)

* 물리 계층을 통해 송수신되는 정보의 오류와 흐름을 관리하여 안전한 정보를 전달하는 역할

* MAC 주소를 가지고 통신

* 데이터 단위 : 프레임

* 대표적인 장비 : 브리지, 스위치

* 프로토콜 종류

  > Ethernet, ATM, 등...

#### 1 계층 - Physical Layer (물리 계층)

* 최하위 계층
* 전기, 기계적 장비를 이용하여 통신 케이블로 데이터 전송(단순 전송)
* 데이터 단위 : 비트
* 대표적인 장비 : 케이블, 리피터, 허브



## :page_with_curl: Reference

[[산업용 이더넷] 산업용 이더넷 네트워크](http://www.hellot.net/new_hellot/magazine/magazine_read.html?code=201&idx=17723&public_date=2014-02)

[OSI 7 계층이란?, OSI 7 계층을 나눈 이유](https://shlee0882.tistory.com/110)

[[네트워크] OSI 7 계층 (OSI 7 LAYER) 기본 개념, 각 계층 설명](https://reakwon.tistory.com/59)

[OSI 7 계층](https://tar-cvzf-studybackup-tar-gz.tistory.com/37)

[OSI 7계층 각 계층의 특징과 역할](https://wiseworld.tistory.com/55)