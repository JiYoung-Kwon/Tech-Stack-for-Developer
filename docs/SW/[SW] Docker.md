# [Docker] Docker

:writing_hand: *Assembled by JiYoung-Kwon (2021-01-16)* 



#### :pushpin: **가상화란?**

- 물리적인 하드웨어 장치를 논리적인 객체로 추상화 하는 것
- 즉, 하나의 자원을 쪼개서 쓰거나, 여러개의 자원을 하나인것 처럼 묶어서 쓸수 있도록 해줌



## 1. 도커(Docker)란?

<img src = https://t1.daumcdn.net/cfile/tistory/9981E6375B8CF0802A width = 50%>

* 2013년 3월 산타클라라에서 열린 Pycon Conference에서 dotCloud의 창업자인 Solomon Hykes가 [The future of Linux Containers](https://youtu.be/wW9CAH9nSLs) 라는 세션을 발표하면서 처음 세상에 알려짐
* Go언어로 작성된 리눅스 **컨테이너 기반**으로 하는 오픈소스 가상화 플랫폼
* 다양한 프로그램, 실행환경을 **컨테이너로 추상화하고 동일한 인터페이스**를 제공하여 프로그램의 배포 및 관리를 단순하게 해줌
* 하나의 서버에 여러 개의 컨테이너가 실행됨에도, 서로 성능에 영향을 끼치지 않고 독립적으로 실행되며 새로운 컨테이너를 생성하는데 고작 1-2초 밖에 걸리지 않는다는 것이 도커의 가장 큰 매력

#### 1-1 컨테이너(Container)란?

![img](https://t1.daumcdn.net/cfile/tistory/99DEAB4D5B652E051B)

* 가상화 기술 중 하나로, 대표적으로 LXC(Linux Container)가 있음

* 기존 OS를 가상화 시키던 것과 달리 **OS레벨의 가상화로, 프로세스를 격리시켜 동작하는 방식**

* 하나의 컴퓨터에 다수의 컨테이너를 실행하면, 각각의 독립된 환경으로 가상 머신을 사용하는 것 같은 느낌을 받을 수 있음

* 장점

  * 가볍고 빠른 실행 속도

    * Hypervisior 엔진을 사용하지 않고 Docker Engine을 사용

      -> Guest OS없이 실행 가능하므로, 더 빠른 속도를 보장

  * 높은 직접도

    * 여러 컨테이너를 만들어 실행 중이어도, OS는 하나이기 때문에 가상머신에 비해 고밀도가 가능
    * 컨테이너는 실행되는 프로세스를 위한 메모리만 사용하기 때문에 낮은 사양에서도 동작 가능

  * 낮은 오버헤드

    * 가상화를 위한 하드웨어 애뮬레이터 단계없이, 분리된 공간을 만들기 때문

* 단점

  * Host OS에 종속적

    * Linux 컨테이너는 OS에서 Linux Kernel이 관리

      -> Linux 이외의 다른 OS에서는 동작하지 않으며, 컨테이너 환경에서도 다른 OS를 설치할 수 없음

    * 실행 중인 커널은 하나이기에, 컨테이너는 호스트 OS의 커널을 사용

  * 컨테이너 별 커널 구성 불가능

    * 컨테이너마다 다른 커널 작업을 수행할 수 없음

#### 1-2. Docker Architecture

![img](https://t1.daumcdn.net/cfile/tistory/996D1D425B8D4F5125)

## 2. Docker vs VM

* **도커(Docker)는 배포에, VM은 환경 테스팅에 초점이 맞춰져있음**
* VM
  * 독립된 커널 공간을 가지는 OS를 구성
  * Hypervisior로 가상머신을 올려서 가상화
* Docker
  * 사용자 공간을 여러 개로 나누어 사용
  * 커널 공간을 공유하여 좀 더 가벼움
  * Docker위에 컨테이너를 올려 가상화
  * 가상화 오버헤드가 거의 발생하지 않음
  * 즉, 가상 머신을 생성하는 것이 아니라 Host OS가 사용하는 자원을 분리하여 여러 환경을 만들 수 있도록 하는 것

![img](https://blog.kakaocdn.net/dn/ebHuea/btqz6u8tRvC/16FMd3Zw5XcK6Bc4ti3iE1/img.png)

<br/>

#### 1. 가상 머신 ex) VMware, VirtualBox

* Host OS 위에 가상화를 시키기 위한 Hypervisor 엔진 그리고 그 위에 Guest OS, 필요한 라이브러리를 올려 사용
* 즉 배포할 각 애플리케이션 스택마다 별도의 VM과 게스트 OS가 필요하고, 이러한 것들은 곧 **성능의 문제와 직결**됨
* 장점 : Host OS와 완전히 분리
* 단점 : OS위에 OS를 올리기 때문에 무겁고 느림

<br/>

#### 2. Linux 위에서의 Docker

* Host Linux 시스템을 사용

* 프로세스 격리를 통해 응용 프로그램 및 종속성을 모듈 식 Container로 패키지함

* VM이 필요하지 않으며, App1과 App2의 OS 리소스는 서로 공유 됨

  -> CPU나 Memory를 딱 필요한 만큼만 할당하게 되고, 성능 손실이 거의 발생하지 않음

<br /> 

#### 3. Linux가 아닌 시스템에서의 Docker

* Docker가 동작하기 위한 미니 Linux가 포함된 경량 VM이 필요
* VM과 비교하여, 컨테이너의 수와 관계없이 단일 VM 및 Guest Linux System만 필요하다는 장점이 있음



## 3. Docker Image

<img src = https://t1.daumcdn.net/cfile/tistory/992AF74C5B8D3D780E width = 50%>

* **컨테이너를 실행할 수 있는 실행파일, 설정 값 등을 가지고 있는 것**
* 상태값을 가지지 않고 변하지 않음
* 컨테이너 == 이미지를 실행한 상태
* 추가되고 변하는 값은 컨테이너에 저장됨
* **장점**
  * 같은 이미지를 여러 개의 컨테이너에서 생성할 수 있고, 컨테이너의 상태가 변경되거나 삭제되어도 **이미지는 변하지 않고 그대로 남아있음**
   - 새로운 서버가 추가되면 미리 만든 **이미지를 다운받고 컨테이너를 생성**하기만 하면 됨
    - 컨테이너를 실행하기 위한 모든 정보를 가지고 있기 때문에 의존성 파일을 컴파일하고 다른 것을 설치할 필요성이 사라짐  

* Docker hub에 등록하거나, Docker Registry 저장소를 직접 만들어 관리할 수 있음
  * 현재 공개된 도커 이미지는 50만개가 넘고, Docker hub의 이미지 다운로드 수는 80억 회
  * 누구나 쉽게 이미지를 만들고 배포할 수 있음
  * ![img](https://t1.daumcdn.net/cfile/tistory/99B173485B8D49AE12)
  * 

#### 3-1. Layer 저장 방식

* 도커 이미지는 컨테이너를 실행하기 위한 모든 정보를 가지고 있어 용량이 엄청 거대함

* 처음 이미지를 다운받으면 크게 부담이 되지 않지만, 기존 이미지에 파일이 하나 추가되었다고 다시 다운받는 것은 비효율적

* 이런 문제를 해결하기 위해 도커는 **레이어(layer)**라는 개념을 도입

* 유니온 파일 시스템을 이용하여 여러 개의 레이어를 하나의 파일 시스템으로 사용할 수 있게 해줌

  ![img](https://t1.daumcdn.net/cfile/tistory/991ACC3C5B8D445C0C)

  * 예시

    > 1. ubuntu 이미지를 만들기 위해 Layer A,B,C가 들어감
    >
    > 2. nginx 이미지 :  ubuntu 이미지를 베이스 이미지로 사용하여 베이스 이미지에 nginx만 더함 ( ubuntu(Layer A,B,C) + nginx )
    >
    > 3. web app 이미지 : ubuntu에 nginx를 올리고 web app을 올리는 것이 아닌, 이미 만들어진 nginx 베이스 이미지에 web app을 올림
    >
    > 4. web app 소스 수정시 a, b, c, nginx 레이어를 제외한 새로운 web app src(v2) 레이어만 다운 받으면 됨
    >
    >    -> 굉장히 효율적으로 이미지를 관리할 수 있음

* 컨테이너를 생성할 때도 레이어 방식을 사용

  * 기존 이미지 레이어 위에 읽기/쓰기(R/W) 레이어를 추가

  * 이미지 레이어를 그대로 사용하면서, 컨테이너가 실행 중에 생성하는 파일이나 변경된 내용은 R/W 레이어에 저장됨

    -> 여러 개의 컨테이너를 생성해도 최소한의 용량만 사용

#### 3-2. Image 경로

![img](https://subicura.com/assets/article_images/2017-01-19-docker-guide-for-beginners-1/image-url.png)

* 이미지는 url 방식으로 관리하며, 태그를 붙일 수 있음
* ubuntu 14.04 이미지는 `docker.io/library/ubuntu:14.04` 또는 `docker.io/library/ubuntu:trusty` 이고 `docker.io/library`는 생략가능하여 `ubuntu:14.04` 로 사용할 수 있음
* 이러한 방식은 이해하기 쉽고 편리하게 사용할 수 있으며 태그 기능을 잘 이용하면 테스트나 롤백도 쉽게 할 수 있음

## :page_with_curl: Reference

[Docker란 무엇인가? 도커에 대해 알아보기](https://judo0179.tistory.com/14)

[[Docker] Docker의 개념 및 핵심 설명](https://khj93.tistory.com/entry/Docker-Docker-개념)

[[Docker] Docker의 개요](https://ooeunz.tistory.com/61)

[[Docker] 개념 정리 및 사용방법까지.](https://cultivo-hy.github.io/docker/image/usage/2019/03/14/Docker%EC%A0%95%EB%A6%AC/)