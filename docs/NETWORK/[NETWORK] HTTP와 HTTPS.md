# [NETWORK] HTTP와 HTTPS

:writing_hand: *Assembled by JiYoung-Kwon (2021-01-12)* 



## 1. HTTP란?

* Hypertext Transfer Protocol의 약자

* 웹브라우저(Client)와 서버(Server) 간 통신을 주고 받게 해주는 가장 기초적인 프로토콜

* 인터넷의 초기에 모든 웹사이트에서 기본적으로 사용되었던 프로토콜

* 주로 HTML 문서를 주고 받을 때 사용

* 80번 포트를 사용함

* 서버에서부터 브라우저로 전송되는 정보가 암호화 되지 않음

  -> **데이터가 쉽게 도난당할 수 있다!** (이 문제를 해결하기 위해 HTTPS 등장)

<br/>

#### 1-1. HTTP의 구조

![img](https://blog.kakaocdn.net/dn/bkdJ4Q/btqK6AXLEtC/jBZzMuJBWzdLYmqILo5Ri1/img.png)

* 애플리케이션 레벨의 프로토콜로, TCP/IP 위에서 작동
* Stateless 프로토콜이며, Method, Path, Version, Headers, Body 등으로 구성됨

<br/>

## 2. HTTPS란?

![img](https://t1.daumcdn.net/cfile/tistory/9989B1505C72885E29)

* Hypertext Transfer Protocol over **Secure** Socket Layer의 약자

* HTTP에 **데이터 암호화가 추가**된 프로토콜

* 443번 포트를 사용함

* **SSL/TLS 프로토콜**을 사용함으로써 HTTP의 보안 문제를 해결

* 네트워크 상에서 중간에 제 3자가 정보를 볼 수 없도록 **공개키 암호화**를 지원

* 실제 전송되는 **데이터**의 암호화에는 대칭키 암호화 방식을 사용, **키 교환**에는 공개키 암호화를 사용

  > 공개키/개인키
  >
  > * 공개키 : 모두에게 공개 가능한 키
  > * 개인키 : 나만 가지고 알고 있어야 하는 키
  >
  > ![img](https://blog.kakaocdn.net/dn/OKcog/btqK71fM8a4/g1HmcDOR7MVRRz7pSKKJWk/img.png)
  >
  > * 공개키 암호화 : 개인키로만 복호화 할 수 있음 
  >
  >   -> 개인키는 나만 가지고 있으므로, 나만 볼 수 있음
  >
  > * 개인키 암호화 : 공개키로만 복호화 할 수 있음
  >
  >   -> 공개키는 모두에게 공개되어 있으므로, 내가 인증한 정보임을 알려 신뢰성을 보장할 수 있음
  >
  > * 처리 속도가 느림
  >
  > 대칭키
  >
  > * 처리속도가 빠르지만, 서버와 클라이언트가 같은 키를 사용해야 함 
  >
  >   -> 키를 공유하는데 문제가 있음

#### 2-2. HTTPS의 동작 과정

* 인증서 발급

<img src= "https://t1.daumcdn.net/cfile/tistory/99F0FA445C456BB809" width = "70%">

> 1. 인터넷 사이트는 자신의 정보와 공개키를 인증기관에 제출
  2. 인증기관은 제출된 데이터 검증절차를 거쳐 개인키로 사이트에서 제출한 정보를 암호화, 인증서 발급
  3. 인증기관은 웹 브라우저에게 자신의 공개키를 제공

* 사용자의 사이트 접속

<img src= "https://t1.daumcdn.net/cfile/tistory/993364345C457AED30" width = "70%">

> 1. 사용자가 사이트에 접속하면, 자신의 인증서를 웹 브라우저에게 보냄
> 2. 웹 브라우저는 미리 받았던 인증기관의 공개키로 인증서를 해독하여 검증 -> 사이트의 정보와 사이트의 공개키를 알게 됨
> 3. 얻은 사이트 공개키로 대칭키를 암호화해 다시 사이트에 보냄
> 4. 사이트는 개인키로 암호문을 해독해 대칭키를 얻게 되고, 이제 대칭키로 데이터를 주고받을 수 있음

<img src="https://t1.daumcdn.net/cfile/tistory/9997354E5C457AF229" width = "70%">

## 3. HTTP vs HTTPS

![img](http://blog.wishket.com/wp-content/uploads/2020/02/03-3.png)

* 보안
  * HTTP : 암호화 X -> 보안에 취약함
  * HTTPS : SSL 인증서, 암호화 -> 안전하게 데이터를 주고 받을 수 있음
* 속도
  * HTTP : 속도가 비교적 빠름
  * HTTPS : 암호화/복호화 과정 필요 -> 비교적 속도가 느림
* 비용
  * HTTP : 추가 비용 X
  * HTTPS : 인증서 발급 및 유지에 필요한 추가 비용 발생

* HTTPS로 전환 시, 검색엔진 최적화(SEO)에 있어서 큰 혜택을 볼 수 있음

  * 보안 문제가 중요해 짐에 따라, 구글에서는 HTTPS를 사용하는 웹 사이트에 대해 검색 순위 결과에 약간의 가산점을 주겠다고 발표하였음
  * 사용자들이 결국에는 가장 안전하다고 생각하는 사이트를 더 많이 방문하기 때문

* 가속화된 모바일 페이지(AMP, Accelerated Mobile Pages)를 만들땐, HTTPS 프로토콜을 사용해야 함

  >  AMP 
  >
  > * 모바일 기기에서 훨씬 빠르게 콘텐츠를 로딩하기 위한 방법, Google이 만듬
  > * HTML에서 불필요한 부분을 없앤 것이라고 볼 수 있음

<br/>

## :page_with_curl: Reference

[HTTP와 HTTPS의 5가지 차이점 정리](https://whatismarketing.tistory.com/61)

[HTTP VS HTTPS 차이, 알면 사이트의 레벨이 보인다.](http://blog.wishket.com/http-vs-https-%EC%B0%A8%EC%9D%B4-%EC%95%8C%EB%A9%B4-%EC%82%AC%EC%9D%B4%ED%8A%B8%EC%9D%98-%EB%A0%88%EB%B2%A8%EC%9D%B4-%EB%B3%B4%EC%9D%B8%EB%8B%A4/)

[[Web] HTTP와 HTTPS 및 차이점](https://mangkyu.tistory.com/98)

[[네트워크]HTTP와 HTTPS의 차이점 그리고 동작 방식](https://devdy.tistory.com/14)

[Http와 Https 이해와 차이점 그리고 오해(?)](https://jeong-pro.tistory.com/89)
