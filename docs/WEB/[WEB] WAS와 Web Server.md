# [WEB] WAS와 Web Server

:writing_hand: *Assembled by JiYoung-Kwon (2021-02-07)* 



## 1. WAS(Web Application Server)

* DB 조회나 다양한 로직 처리를 요구하는 **동적인 컨텐츠를 제공**하기 위해 만들어진 Application Server
* HTTP를 통해 컴퓨터나 장치에 애플리케이션을 수행해주는 **미들웨어**
  * 미들웨어 : 운영 체제와 응용 소프트웨어의 중간에서 조정과 중개의 역할을 수행하는 소프트웨어
* '웹 컨테이너' or '서블릿 컨테이너'라고도 불림
  - 즉, JSP, Servlet 구동 환경을 제공함

<br/>

#### 1-1. 역할

- WAS = Web Server + Web Container
- Web Server의 기능들을 구조적으로 분리하여 처리하고자는 목적으로 제시됨
  - 분산 트랜잭션, 보안, 메시징, 쓰레드 처리 등의 기능을 처리하는 분산 환경에서 사용됨
  - 주로 DB 서버와 같이 수행됨
- 현재는 WAS가 가지고 있는 Web Server도 정적인 컨텐츠를 처리하는데 있어서 **성능상 큰 차이가 없음**

<br/>

#### 1-2. 기능

1. 프로그램 실행 환경과 DB 접속 기능 제공

2. 여러 개의 트랜잭션(논리적 작업 단위) 관리 기능

3. 업무를 처리하는 비즈니스 로직 수행

<br/>

#### 1-3. 예

* Tomcat(대표적), JBoss, Jeus, Web Sphere 등

<br/>

------

*즉, WAS의 경우 웹 서버 + 웹 컨테이너의 개념으로 웹서버의 역할을 동시에 할 수 있다는 것이다. 그렇다면 웹서버를 사용하지 않고 WAS만 쓰면 되는 것 아닌가?*

<br/>

## 2. Web Server

* 소프트웨어와 하드웨어로 구분됨

  - 하드웨어 : Web 서버가 설치되어 있는 컴퓨터
  - 소프트웨어 : 웹 브라우저 클라이언트로부터 HTTP 요청을 받아 **정적인 컨텐츠(.html .jpeg .css 등)를 제공**하는 서버

<br/>

#### 2-1. 기능

  - HTTP 프로토콜을 기반으로 하여 클라이언트(웹 브라우저)의 요청을 서비스하는 기능을 담당
  - 요청에 따라 두가지 기능 중 적절하게 선택하여 수행함
    1. 정적인 컨텐츠 제공
       - WAS를 거치지 않고 바로 자원을 제공함
    2. 동적인 컨텐츠 제공을 위한 요청 전달
       - 클라이언트(웹 브라우저)의 요청(Request)을 WAS에 보내고, WAS가 처리한 결과를 클라이언트(웹 브라우저)에게 전달함

<br/>

#### 2-2. 예

- Apache Server(대표적), Niginx, IIS(Window 전용 Web 서버) 등

<br/>

## 3. Web Server와 WAS를 나눠야 하는 이유

#### 1. 서버 부하 방지

- WAS는 DB조회나 다양한 로직을 처리하느라 바쁘기 때문에 단순한 정적 컨텐츠는 Web Server에서 빠르게 클라이언트에게 제공하여 처리하는 것이 좋음
- WAS는 기본적으로 동적 컨텐츠를 제공하기 위해 존재하는 서버
- 만약, WAS가 정적 컨텐츠 요청까지 처리하게 된다면, 부하가 커지고 동적 컨텐츠 처리가 지연되면서 수행속도가 느려져 이로 인해 페이지 **노출 시간이 늘어나는 문제가 발생** 하여 **효율성이 크게 떨어짐**

#### 2. 물리적 분리로 보안 강화

- WAS의 경우 DB서버에 대한 접속 정보가 있기 때문에 외부로 노출될 경우 보안상 문제가 될 수있음
- SSL에 대한 암복호화 처리에 Web Server를 사용

#### 3. 여러대의 WAS 연결 가능

- *Load Balancing*을 위해 Web Server 사용
  - **Load Balancing**
    - 부하분산이라고 하며, 컴퓨터 네트워크 기술의 일종으로 둘 또는 셋 이상의 중앙처리장치 혹은 저장장치와 같은 컴퓨터 자원들에게 작업을 나누는 것
- fail over(장애 극복), fail back(장애 전 상태) 처리에 유리
- 특히 대용량 웹 어플리케이션의 경우 여러개의 서버를 사용, Web Server와 WAS를 분리하여 무중단 운영을 위한 장애 극복에 쉽게 대응할 수 있음
  - ex) 앞단의 Web Server에서 오류가 발생한 WAS를 이용하지 못하도록 한 후 WAS를 재시작하여 사용자는 오류를 느끼지 못하고 이용할 수 있음

#### 4. 여러 웹 어플리케이션 서비스 가능

- 하나의 서버에서 PHP Application과 Java Application을 함께 사용할 수 있음

#### 5. 기타

- 접근 허용 IP 관리, 2대 이상의 서버에서의 세션 관리 등도 Web Server에서 처리하면 효율적임

<br/>

즉, **자원 이용의 효율성 및 장애 극복, 배포 및 유지보수의 편의성**을 위해 Web Server와 WAS를 분리함

------

***Web Server를  WAS 앞에 두고 필요한  WAS들을  Web Server에 플러그인 형태로 설정하면 더욱 효율적인 분산 처리가 가능하다.***

------

<br/>

## 4. Web Service Architecture

#### 4-1. Client -> Web Server -> DB

![img](https://user-images.githubusercontent.com/58902042/106453546-d5eb3680-64cc-11eb-94f2-175a47ceb3f5.PNG)

- Web Server는 파일 경로 이름을 받아 경로와 일치하는 file contents를 반환함
- 항상 동일한 페이지를 반환함
- ex) image, html, css, javascript 파일과 같이 컴퓨터에 저장되어있는 파일들

<br/>

#### 4-2. Client -> WAS -> DB

![img](https://user-images.githubusercontent.com/58902042/106453771-22cf0d00-64cd-11eb-8298-e249c7af8baf.PNG)

- 인자의 내용에 맞게 동적인 contents를 반환함
- 사용자의 요청을 Servlet에서 동적으로 처리하여 모든 사용자를 서로 다른 결과를 서버로부터 응답받음

<br/>

#### 4-3. Client -> Web Server -> WAS -> DB

- 이 구조의 동작 과정

  ![img](https://user-images.githubusercontent.com/58902042/106428922-0fac4500-64ad-11eb-884a-c9f135111000.png)

  1. Web Server는 웹 브라우저 클라이언트로부터 HTTP 요청을 받는다.

  2. Web Server는 클라이언트의 요청(Request)을 WAS로 보낸다.

  3. WAS는 관련된 Servlet을 메모리에 올린다.

  4. WAS는 web.xml을 참조하여 해당 Servlet에 대한 Thread를 생성한다. (Thread Pool 이용)

  5. HttpServletRequest와 HttpServletResponse 객체를 생성하여 Servlet에 전달한다.

     5-1. Thread는 Servlet의 service() 메서드를 호출한다.

     5-2. service() 메서드는 요청에 맞게 doGet() 또는 doPost() 메서드를 호출한다.

     - protected doGet(HttpServletRequest request, HttpServletResponse response)

  6. doGet() 또는 doPost() 메서드는 인자에 맞게 생성된 적절한 동적 페이지를 Response 객체에 담아 WAS에 전달한다.

  7. WAS는 Response 객체를 HttpResponse 형태로 바꾸어 Web Server에 전달한다.

  8. 생성된 Thread를 종료하고, HttpServletRequest와 HttpServletResponse 객체를 제거한다.

<br/>

#### :pushpin: Apache Tomcat

* 정적 컨텐츠를 처리하는 웹서버는 Apache, 동적 컨텐츠를 처리하는 WAS에는 Tomcat
* 실제로는 Apache Tomcat이라는 이름으로 사용되어 혼란스러움
  * 2008년에 릴리즈 된 Tomcat 5.5 버전부터 정적 컨텐츠를 처리하는 기능이 추가되었는데, 이 기능이 순수 Apache를 사용하는 것에 비해 성능적 차이가 전혀 없으며 Tomcat이 Apache의 기능을 포함하고 있기 때문에 Apache Tomcat이라고 부르고 있음

<br/>

## :page_with_curl: Reference

[[web] Web Server와 WAS의 차이와 웹서비스 구조](https://gmlwjd9405.github.io/2018/10/27/webserver-vs-was.html)

[WAS(Web Application Server)란?](https://goldsony.tistory.com/37)

[WAS 와 웹 서버 차이 (WAS,Web Server) 그리고 아파치, 톰캣](https://jeong-pro.tistory.com/84)

[[Web] 웹 서버와 WAS의 차이를 쉽게 알아보자](https://codechasseur.tistory.com/25)

[로드밸런싱이란 무엇인가](https://oriyong.tistory.com/94)

[미들웨어-wiki](https://ko.wikipedia.org/wiki/미들웨어)