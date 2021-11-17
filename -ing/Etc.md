# 개념 정리

😄 작성자 : 권지영 😄

## 1. Typesafe

* 참고 : https://gtilog.netlify.app/devLogs/java/20170328-java-hocon-usage

* java properties, json, json superset(ex- hocon)과 같은 설정 파일을 읽기 위한 **configuration library**

* 프로젝트 설정 정보 파일을 통해 설정 정보를 읽어올 수 있음

* ```java
  ConfigFactory.load()
  /* 
  설정 파일을 불러옴 (다음과 같은 이름을 가진 클래스 경로의 모든 리소스)
  * system properties
  * application.conf
  * application.json
  * application.properties
  * reference.conf
  */
    
  resolve()
  // ${foo.bar}가 해결된 대체 구성 반환
  // 즉, getValue("foo.bar")의 결과로 대체된다는 것
  // ex) modbus{path = "dfdf/eqwd"} => modbus.getValue
  ```



## 2.File

* 참고 : https://veloper.tistory.com/55

* ```java
  File(String pathname)
  // 주어진 pathname을 경로로 하는 새로운 파일 객체를 생성
    
  // 메소드
  isDirectory() // File 객체가 디렉토리를 참조하는지를 테스트함
    
  ```



## 3. JPA

* 참고 : https://gmlwjd9405.github.io/2019/08/04/what-is-jpa.html

* 참고2 : https://velog.io/@adam2/JPA%EB%8A%94-%EB%8F%84%EB%8D%B0%EC%B2%B4-%EB%AD%98%EA%B9%8C-orm-%EC%98%81%EC%86%8D%EC%84%B1-hibernate-spring-data-jpa

* ORM

  * Object-relational mapping (객체 관계 매핑)
  * 객체는 객체대로 설계하고, 관계형 데이터베이스는 관계형 데이터대로 설계한다.
  * ORM 프레임워크가 중간에서 매핑해줌
  * 객체 간의 관계를 바탕으로 SQL을 자동으로 생성해줌

* JPA(Java Persistence API)

  * 현재 자바 진영의 ORM 기술 표준, 인터페이스의 모음

  * 실제로 동작하는 것이 아님

    * JPA 인터페이스를 구현한 대표적인 오픈소스가 Hibernate

      > Hibernate : ORM 프레임워크, Open Source SW

    * 이외에, EclipseLink, DataNucleus 등이 있음

* 동작과정

  * ![img](https://media.vlpt.us/images/adam2/post/cde32cd8-b9c0-49c4-bf99-b58c0b0c2e18/Untitled%203.png)
  * 애플리케이션과 JDBC 사이에서 동작한다.
  * 개발자가 JPA를 사용하면, JPA 내부에서 JDBC API를 사용하여 SQL을 호출하여 DB와 통신한다.
  * 즉, 개발자가 직접 JDBC API를 쓰는 것이 아님

* 특징

  1. 데이터를 객체지향적으로 관리할 수 있다.
     * 개발자는 비즈니스 로직에 집중할 수 있고, 객체지향 개발이 가능하다.
  2. 자바 객체와 DB 테이블 사이의 매핑 설정을 통해 SQL을 생성한다.
  3. 객체를 통해 쿼리를 작성할 수 있는 JPQL(Java Persistence Query Language)을 지원
  4. 성능 향상을 위해 지연 로딩이나 즉시 로딩과 같은 몇가지 기법을 제공함
     * 잘 활용하면, SQL을 직접 사용하는 것과 유사한 성능을 얻을 수 있다.

* 왜 사용해야 할까!?

  1. SQL 중심적인 개발 -> 객체 중심적인 개발
  2. 생산성 증가 ; 간단한 메소드로 CRUD가 가능함
  3. 유지보수가 쉬움
     * 기존 : 필드 변경 시, 모든 SQL을 수정해야 함
     * JPA : 필드만 추가하면 됨 (SQL은 JPA가 처리하기 때문)
  4. Object와 RDB 간의 패러다임 불일치 해결



## 4. Akka HTTP

* HTTP 기반 서비스를 제공하고 사용하기 위한 일반 툴킷 제공
* akka-actor, akka-stream 위에 전체 서버 및 클라이언트 측 HTTP 스택 구현











