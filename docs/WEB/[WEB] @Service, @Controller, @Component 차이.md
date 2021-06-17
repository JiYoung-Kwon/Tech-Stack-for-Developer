# [WEB] @Service, @Controller, @Component 차이

✍️ *Assembled by JiYoung-Kwon (2021-06-18)*

* spring task scheduler 코드 구현 중, 자바 클래스에 @Service / @Controller / @Component 각각을 붙였을 때 동일한 결과를 출력하는 것을 경험하였고, 각각의 차이에 대해서 궁금증이 생김



## 1. Stereo Type(스테레오 타입)

* 스프링 컨테이너가 스프링 관리 컴포넌트로 식별하게 해주는 단순한 마커

  * 즉, scan-auto-detection과 dependency injection을 사용하기 위해서 사용되는 가장 기본 어노테이션

* Stereo Type이 범용적으로 많이 사용하게 된 시기는 Spring 2.5 부터
  * 그 이전까지는 xml 파일에 bean을 등록하여 관리 
    * 모든 bean들을 xml 파일로 관리하다 보니, 다른 보일러플레이트 코드와 함께 xml 파일만 비대해지게 될 뿐이었음
  * 그래서 Spring 2.0 에서는 @Repository이 등장
  *  Spring 2.5 부터는 @Component, @Controller, @Service, @Configuration 등이 등장하면서 Stereo type에 대한 정의가 범용적으로 사용됨


* ![img](https://blog.kakaocdn.net/dn/bpiV1F/btquzHydBKR/yb6QJY3SCFKsVhFveEJlRk/img.png)
* ![img](https://gblobscdn.gitbook.com/assets%2F-M5HOStxvx-Jr0fqZhyW%2F-MGRXqsY8lYe9idKp2rD%2F-MGRcDp1KGXVW9BE_0n7%2F%E1%84%80%E1%85%B3%E1%84%85%E1%85%B5%E1%86%B71.png?alt=media&token=9837df71-c882-4639-979f-774dd90f8c61)

<br/>

## 2. @Component

* 빈으로 간주되어 DI 컨테이너에서 사용할 수 있게 하는 기본 어노테이션
* 스프링에서 관리되는 객체임을 표시하기 위해 사용하는 가장 기본적인 annotation

<br/>

#### @Bean과 @Component의 차이

* @Component

  * 클래스 상단에 적으며, 그 default로 **클래스 이름이** bean의 이름이 됨
  * spring에서 자동으로 찾고(@ComponentScan 사용) 관리해주는 bean

* @Bean
  * @Configuration으로 선언된 클래스 내에 있는 메소드를 정의할 때 사용
  * **이 메소드가 반환하는 객체가 bean이 되며** default로 **메소드 이름이** bean의 이름이 됨

<br/>

## 3. @Controller

* Web MVC 코드에 사용되는 어노테이션
* Dispatcher Servlet에서 제공됨
* @RequestMapping 어노테이션을 해당 어노테이션 밑에서만 사용할 수 있음
  * 이 어노테이션을 사용하여 클라이언트 요청을 특정 컨트롤러에 전달할 수 있게 해줌

<br/>

#### @RestController와 @Controller의 차이

* @RestController
  * Spring 3.0 에서 추가된 어노테이션
  * RESTful web service를 제공하기 위해 @Controller를 확장한 개념
* 기능적인 측면에서 보았을 땐, @Controller에 @ResponseBody 어노테이션이 추가된 기능이라고 보면 됨

* @ResponseBody 
  * 결과값이 View를 통해서 출력되지 않고, HTTP Response Body에 직접 쓰여지게 됨
  * 이때 리턴되는 데이터 타입에 따라 MessageConverter에서 변환이 이뤄진 후 쓰여지게 됨

<br/>

## 4. @Service

* 단순히 서비스 레이어에서 사용하는 bean이라는 것을 구분하기 위한 용도로 정의
  * 비즈니스 로직이나 Repository layer 호출하는 함수에 사용됨
  * 다른 어노테이션과 다르게 @Component에 추가된 기능은 없음
* @Component로 대체해도 무방하지만 권장하지는 않음
  * 나중에 Spring 측에서 추가적인 exception handling을 해줄 수도 있으니, 비즈니스 로직에는 해당 어노테이션을 사용하는 것을 권장

<br/>

## 5. @Repository

* 검사 되지 않은 예외(DAO 메소드에서 발생)를 Spring DataAccessException으로 변환 할 수 있게 해줌

  * 플랫폼 별 예외를 잡아서 Spring의 통합검사되지 않은 예외 중 하나로 다시 던지는 것

* 이를 위해 PersistenceExceptionTranslationPostProcessor이 제공되며, 다음과 같이 Spring의 ApplicationContext에 추가해야 함

  ```xml
  <bean class ="org.springframework.dao.annotation.PersistenceExceptionTranslationPostProcessor"/>
  ```

  * 이 bean PostProcessor은 @Repository로 주석이 달린 모든 빈에 권고자를 추가하여, 플랫폼 별 예외를 포착한 다음 Spring의 통합검사되지 않은 예외 중 하나로 다시 발생시킴

<br/>

## 6. @Configuration

* 한 개 이상의 @Bean 어노테이션으로 정의한 bean들을 생성하려 할 때, 클래스에 정의하는 어노테이션

<br/>

#### @Bean은 언제 사용하는게 좋을까?

- 개발자가 직접 제어가 불가능한 라이브러리를 활용할 때 사용
- 초기에 설정을 하기 위해 활용할 때 사용



## :page_with_curl: Reference

[Stereo Type(스테레오 타입)](https://incheol-jung.gitbook.io/docs/q-and-a/spring/stereo-type)

[[카카오 면접] @Service, @Controller, @Component 차이](https://bk-investing.tistory.com/64)

[Spring annotation - @Service,@Controller,@Component 차이](https://happyer16.tistory.com/entry/Spring-annotation-ServiceControllerComponent-%EC%B0%A8%EC%9D%B4)