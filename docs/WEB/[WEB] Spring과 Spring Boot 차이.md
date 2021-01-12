# [WEB] Spring과 Spring Boot 차이

:writing_hand: *Assembled by JiYoung-Kwon (2021-01-11)* 



#### :pushpin: 프레임워크 vs 라이브러리

  * 프레임워크(Framework)

    > * SW의 특정 문제를 해결하기 위해 상호 협력하는 클래스와 인터페이스의 집합
    >
    > * 완성된 어플리케이션이 아닌 프로그래머가 완성시키는 작업을 해야함
    > * 객체 지향 개발을 하게 되면서 통합성, 일관성의 부족이 발생되는 문제를 해결할 방법 중 하나
    > * 라이브러리를 포함하는 개념

* 라이브러리(Library)

  > * 단순 활용가능한 도구들의 집합
  >
  > * 개발자가 만든 클래스에서 호출하여 사용

* 차이

  > * Flow(흐름)에 대한 제어 권한이 누구에게/어디에 있는가
  >
  > * 프레임워크 : 전체적인 흐름을 스스로가 쥐고 있으며, 사용자는 그 안에서 필요한 코드를 짜 넣음 (제어의 역전. IOC, Inversion Of Control)
  >
  >   ```
  >   제어의 역전
  >   - 어떠한 일을 하도록 만들어진 프레임워크에 제어의 권한을 넘김으로써 클라이언트 코드가 신경 써야 할 것을 줄이는 전략
  >   ```
  >
  > * 라이브러리 : 사용자가 전체적인 흐름을 만들며, 라이브러리를 가져다 쓰는 것

  ![img](https://t1.daumcdn.net/cfile/tistory/2344774D577B359522)

  <br/>

## 1. 스프링(Spring)이란?

* Spring, 정확하게는 **Spring Framework**

* 자바 플랫폼을 위한 오픈소스 애플리케이션 프레임워크

  > **애플리케이션 프레임워크**
  >
  > * 특정 계층이나, 기술, 업무 분야에 국한되지 않고 애플리케이션의 전 영역을 포괄하는 프레임워크

* 동적인 웹 사이트를 개발하기 위한 여러 가지 서비스 제공
* 개발자가 코드 안에 애플리케이션 동작에 대한 내용을 기술하면, 스프링 프레임워크가 이를 해석해서 동작

#### 1-1. 스프링의 장점

* 경량 컨테이너
* IOC (Inversion of Control) : 제어 역행
* DI (Dependency Injection) : 의존성 주입
* AOP (Aspect-Oriented Programming) : 관점 지향 프로그래밍

-> 좀 더 결합도를 낮추는 방식으로 애플리케이션을 개발할 수 있음

#### 1-2. 스프링의 단점

* "스프링은 설정이 반이다." 라는 말이 있을 정도로 설정하는 것에 어려움이 많음

  :arrow_right: **스프링 부트**의 탄생

<br/>

## 2. 스프링 부트(Spring Boot)란?

* 스프링 프레임워크의 복잡한 환경설정에 어려움을 느끼는 사용자를 위해 나옴
* 환경 설정의 많은 부분을 **자동화**함 -> 사용자가 스프링을 활용할 수 있도록 도와주어 생산성을 크게 향상함
* 실행환경이나 의존성 관리 등의 인프라 관련 등은 신경쓸 필요 없이 바로 **코딩**을 시작하게끔 도와줌
* **스프링 부트는 스프링 프레임워크라는 큰 틀에 속하는 도구**

![img](https://blog.kakaocdn.net/dn/qABrf/btqzKGVJXYN/o9usekO2gtAkI3tv2oKF5k/img.png)

#### 2-2. Spring framework과의 차이점

1. Embed Tomcat을 사용 (Spring Boot 내부에 Tomcat이 포함되어 있음)

   > * 따로 Tomcat을 설치하거나 매번 버전을 관리해 주어야 하는 수고로움을 덜어줌

2. starter을 통한 dependency 자동화

   > * 과거 Spring framework에서는 각각의 dependency들의 호환되는 버전을 일일이 맞춰줘야 했음
   >
   > * 하나의 버전을 올리고자 하면 다른 dependency에 까지 영향을 미쳐 version관리에 어려움이 많았음
   >
   -> starter가 대부분의 dependency를 관리해주기 때문에 이러한 걱정을 많이 덜게 됨

3. XML설정을 하지 않아도 됨

4. jar file을 이용해 자바 옵션만으로 손쉽게 배포가 가능

5. Spring Actuator를 이용한 애플리케이션의 모니터링과 관리를 제공



## :page_with_curl: Reference

[Spring과 Spring Boot 차이](https://velog.io/@rosa/Spring%EA%B3%BC-Spring-Boot-%EC%B0%A8%EC%9D%B4)

[프레임워크와 라이브러리의 차이점](https://webclub.tistory.com/458)

[[Spring] Spring Framework vs Spring Boot](https://ooeunz.tistory.com/56)

[[Spring] Spring 과 Spring Boot](https://monkey3199.github.io/develop/spring/2019/04/14/Spring-And-SpringBoot.html)