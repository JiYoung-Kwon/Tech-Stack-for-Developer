# [NETWORK] REST API (RESTful)

:writing_hand: *Assembled by JiYoung-Kwon (2021-01-24)* 



## 1. REST란?

* **Representational State Transfer**의 약자

* 자원을 이름(자원의 표현)으로 구분하여 해당 자원의 상태(정보)를 주고 받는 모든 것을 의미

* 즉, **자원의 표현에 의한 상태 전달**

  > **자원**
  >
  > - 해당 소프트웨어가 관리하는 모든 것
  > - ex) 문서, 그림, 데이터, 해당 소프트웨어 자체 등
  >
  > **자원의 표현**
  >
  > - 그 자원을 표현하기 위한 이름
  > - ex) DB의 **학생 정보**가 자원일 때, **'students'**를 자원의 표현으로 정함
  >
  > **상태(정보) 전달**
  >
  > - 데이터가 요청되어지는 시점에서 자원의 상태를 전달함
  > - JSON 혹은 XML을 통해 데이터를 주고 받는 것이 일반적

* REST 아키텍처

  * 월드 와이드 웹 (WWW)와 같은 분산 하이퍼미디어 시스템을 위한 소프트웨어 아키텍처의 한 형식
  
  * REST는 기본적으로 웹의 기존 기술과 HTTP 프로토콜을 그대로 활용하기 때문에 **웹의 장점을 최대한 활용할 수 있는 아키텍처**
  
  * REST는 네트워크 상에서 클라이언트와 서버 사이의 통신 방식 중 하나
* REST의 구체적인 개념

  - HTTP URI를 통해 자원을 명시하고, HTTP Method(Post, Get, Put, Delete)를 통해 해당 자원에 대한 CRUD Operation을 적용하는 것
    
  - REST는 자원 기반의 구조 (ROA, Resource Oriented Architecture) 설계의 중심에 Resource가 있고 HTTP Method를 통해 Resource를 처리하도록 설계된 아키텍처
    
  - 웹 사이트의 이미지, 텍스트, DB 내용 등의 모든 자원에 고유한 ID인 HTTP URI를 부여함
    
    > CRUD Operation
    >
    > - Create : 생성 (POST)
    > - Read : 조회 (GET)
    > - Update : 수정 (PUT)
    > - Delete : 삭제 (DELETE)
    > - HEAD : header 정보 조회 (HEAD)

<br/>

## 2. REST의 장단점

  - **장점**

    - HTTP 프로토콜의 인프라를 그대로 사용

      -> REST API 사용을 위한 별도의 인프라를 구축할 필요가 없음

    - HTTP 프로토콜의 표준을 최대한 활용하여 여러 추가적인 장점을 함께 가져갈 수 있음

    - HTTP 표준 프로토콜에 따르는 모든 플랫폼에서 사용 가능

    - 하이퍼미디어 API의 기본을 충실히 지키면서 범용성을 보장

    - REST API 메시지가 의도하는 바를 명확하게 나타내므로 의도하는 바를 쉽게 파악할 수 있음

    - 여러가지 서비스 디자인에서 생길 수 있는 문제를 최소화함

    - 서버와 클라이언트의 역할을 명확하게 분리
  - **단점**

    - 표준이 존재하지 않음
    - 사용할 수 있는 메소드가 4가지 밖에 없음
      - HTTP Method 형태가 제한적임
      - 브라우저를 통해 테스트할 일이 많은 서비스라면 쉽게 고칠 수 있는 URL보다 Header 값이 왠지 더 어렵게 느껴짐
    - 구형 브라우저가 아직 제대로 지원해주지 못하는 부분이 존재
      - PUT, DELETE를 사용하지 못하는 점 등

## 3. REST가 필요한 이유, 구성요소, 특징

#### 3-1. REST가 필요한 이유

* 애플리케이션 분리 및 통합
* 다양한 클라이언트의 등장
* 최근 서버 프로그램은 다양한 브라우저, 모바일 디바이스에서도 통신을 할 수 있어야 함
* 이러한 멀티 플랫폼에 대한 지원을 위해 서비스 자원에 대한 아키텍처를 세우고 이용하는 방법을 모색한 결과, REST에 관심을 가지게 되었음

<br/>

#### 3-2. 구성요소

- 자원(Resource) : URI
  - 모든 자원에 고유한 ID가 존재하고, 이 자원은 서버에 존재함
  - 자원을 구별하는 ID : '/groups/:group_id'와 같은 HTTP **URI**
  - 클라이언트는 URI를 이용하여 자원을 지정하고 해당 자원의 상태에 대한 조작을 서버에 요청함
- 행위 (Verb) : HTTP Method
  - HTTP 프로토콜의 메소드 **GET, POST, PUT, DELETE**를 사용
- 표현(Representation of Resource)
  - 클라이언트가 자원의 상태에 대한 조작을 요청하면 서버는 이에 적절한 응답(Representation)을 보냄
  - REST에서 하나의 자원은 JSON, XML, TEXT, RSS 등 여러 형태의 표현으로 나타내어 질 수 있음
  - JSON 혹은 XML로 데이터를 주고 받는 것이 일반적임

<br/>

#### 3-3. REST의 특징

- **서버-클라이언트 구조**

    - 자원 있는 쪽이 Server, 자원 요청하는 쪽이 Client
        - REST Server : API를 제공하고 비즈니스 로직 처리 및 저장을 책임짐
        - Client : 사용자 인증이나 context(세션, 로그인 정보) 등을 직접 관리하고 책임짐
    - 서로 간의 의존성이 줄어듦

- **Stateless (무상태)**

  - HTTP 프로토콜 : Stateless Protocol

    -> REST 역시 무상태성을 가짐

  - 클라이언트의 context를 서버에 저장하지 않음

    -> 세션과 쿠키같은 context 정보를 신경쓰지 않아도 되므로 구현이 단순해짐

  - 서버는 각각의 요청을 완전히 별개의 것으로 인식하고 처리

    - 각 API 서버는 클라이언트의 요청만을 단순 처리
  - 이전 요청이 다음 요청의 처리에 연관되어서는 안됨
    
    - 단, 이전 요청이 DB를 수정하여 DB에 의해 바뀌는 것은 허용
  - 서버의 처리 방식에 일관성을 부여하고 부담이 줄어들며, 서비스의 자유도가 높아짐

- **Cacheable (캐시 처리 가능)**

  \* cache : 자주 사용하는 데이터나 값을 미리 복사해 놓는 임시 저장소

  - 웹 표준 HTTP 프로토콜을 그대로 사용하므로 웹에서 사용하는 기존의 인프라를 그대로 활용할 수 있음
    
    - 즉, HTTP가 가진 강력한 특징 중 하나인 캐싱 기능을 적용할 수 있음
    - HTTP 프로토콜 표준에서 사용하는 Last-Modified 태그나 E-Tag를 이용하면 캐싱 구현이 가능함
    
  - 대량의 요청을 효율적으로 처리하기 위해 캐시가 요구됨

  - 캐시 사용을 통해 응답 시간이 빨라지고 REST 서버 트랜잭션이 발생하지 않음

    -> 전체 응답시간, 성능, 서버의 자원 이용률을 향상시킬 수 있음

- **Layered System (계층화)**

  - 클라이언트는 REST API 서버만 호출함

  - REST 서버는 다중 계층으로 구성될 수 있음

    - API 서버는 순수 비즈니스 로직을 수행하고 그 앞단에 보안, 로드밸런싱, 암호화, 사용자 인증 등을 추가하여 구조상의 유연성을 줄 수 있음

    - 또한 로드 밸런싱 공유 캐시 등을 통해 확장성과 보안성을 향상시킬 수 있음

      \* 로드밸런싱 : 컴퓨터 네트워크 기술의 일종으로 둘 혹은 셋이상의 중앙처리장치 혹은 저장장치와 같은 컴퓨터 자원들에게 작업을 나누는 것을 의미

  * Proxy, 게이트웨이 같은 네트워크 기반의 중간 매체를 사용할 수 있음

- **Code-On-Demand (optional)**

  \* code on demand : 사용자가 어떤 프로그램을 자기 단말기로 다운로드 받기를 원하면 그때 시스템에 의해 Java 프로그램이 컴파일되어 해당 단말기에서 실행되는 바이너리로 생성되어 다운로드되는 것

    - 서버로부터 스크립트를 받아서 클라이언트에서 실행함
  
  - 반드시 충족할 필요는 없음
  
* **Uniform Interface (인터페이스 일관성)**
    * URI로 지정한 자원에 대한 조작을 통일되고 한정적인 인터페이스로 수행
  * HTTP 표준 프로토콜에 따르는 모든 플랫폼에서 사용이 가능
    * 특정 언어나 기술에 종속되지 않음

<br/>

## 4. REST API

#### 4-1. REST API (RESTful API) 란?

- REST 기반으로 서비스 API를 구현한 것

  > API
  >
  > ```
  > 데이터와 기능의 집합을 제공하여 컴퓨터 프로그램 간 상호작용을 촉진하며,
  > 서로 정보를 교환 가능하도록 하는 것
  > ```
  >
- 최근 OpenAPI , 마이크로 서비스 등을 제공하는 업체 대부분은 REST API를 제공함

  * Open API : 누구나 사용할 수 있도록 공개된 API ex) 구글 맵
* 마이크로 서비스 : 하나의 큰 애플리케이션을 여러 개의 작은 애플리케이션으로 쪼개어 변경과 조합이 가능하도록 만든 아키텍처

<br/>

#### 4-2. REST API의 특징

- 사내 시스템들도 REST 기반으로 시스템을 분산해 확장성과 재사용성을 높여 유지보수 및 운용을 편리하게 할 수 있음
- REST는 HTTP 표준을 기반으로 구현
  - HTTP를 지원하는 프로그램 언어로 클라이언트와 서버를 구현할 수 있음
- 즉, REST API를 제작하면 델파이 클라이언트 뿐 아니라 자바, C#, 웹 등을 이용해 클라이언트를 제작할 수 있음

<br/>

#### 4-3. REST API 디자인 가이드

**REST API 설계 기본 규칙**

참고) 리소스 원형

> * 도큐먼트 : 객체 인스턴스나 데이터베이스 레코드와 유사한 개념
> * 컬렉션 : 서버에서 관리하는 디렉터리라는 리소스
> * 스토어 : 클라이언트에서 관리하는 리소스 저장소

1. URI는 정보의 자원을 표현해야 한다. 
   * 리소스 명 : 동사보다는 **명사**, 대문자보다는 소문자 사용
   * 도큐먼트 이름 : 단수 명사 사용
   * 컬렉션 이름 : 복수 명사 사용
   * 스토어 이름 : 복수 명사
2. 자원에 대한 행위는 HTTP Method(GET, PUT, POST, DELETE)로 표현
   * URI에 HTTP Method가 들어가면 안됨
     * `GET /members/delete/1` -> `DELETE /members/1`
   * URI에 행위에 대한 동사표현이 들어가면 안됨 (CRUD 기능을 나타내는 것)
     * `GET /members/show/1/` -> `GET /members/1`
     * `GET /members/insert/2` -> `POST /members/2`
   * 경로 부분 중 변하는 부분은 유일한 값으로 대체함 (:id는 하나의 특정 resource를 나타내는 고유값)
     * student를 생성하는 route : POST /students
     * id=12인 student를 삭제하는 route : DELETE /students/12

**URI 설계 시 주의할 점**

1. 슬래시 구분자(/)는 계층 관계를 나타내는 데 사용

```
  http://restapi.example.com/houses/apartments
  http://restapi.example.com/animals/mammals/whales
```

2. URI 마지막 문자로 슬래시를 포함하지 않음

```
  http://restapi.example.com/houses/apartments/ (x)
  http://restapi.example.com/houses/apartments (o)
```
3. 하이픈은 URI 가독성을 높이는데 사용
   * 불가피하게 긴 URI를 사용하게 된다면 사용

4. 밑줄은 URI에 사용하지 않음

5. URI 경로는 소문자로 작성

6. 파일 확장자는 URI에 포함시키지 않음
```
  http://restapi.example.com/members/soccer/345/photo.jpg (X)
```

7. 리소스 간에는 연관 관계가 있는 경우
   * /리소스명/리소스ID/관계가 있는 다른 리소스명

<br/>

## 5. RESTful

#### 5-1. RESTful이란

* 일반적으로 REST라는 아키텍처를 구현하는 웹 서비스를 나타내기 위해 사용되는 용어
  * ‘REST API’를 제공하는 웹 서비스를 ‘RESTful’하다고 할 수 있음
* RESTful은 **REST를 REST답게 쓰기 위한 방법**으로, 누군가가 공식적으로 발표한 것이 아님
  * 즉, REST 원리를 따르는 시스템은 RESTful이란 용어로 지칭됨

#### 5-2. RESTful의 목적

* 이해하기 쉽고 사용하기 쉬운 REST API를 만드는 것

* RESTful한 API를 구현하는 근본적인 목적

  * 일관적인 컨벤션을 통한 API의 이해도 및 호환성을 높이는 것

    -> 성능이 중요한 상황에서는 굳이 구현할 필요가 없음

#### 5-3. RESTful 하지 못한 경우

* CRUD 기능을 모두 POST로만 처리하는 API
* route에 resource, id 외의 정보가 들어가는 경우 (/students/updateName)



## :bulb: 예상질문

Q1 - REST API란 무엇인가요?

A1 - REST를 기반으로 서비스 API를 구현한 것입니다.

<br/>

Q2 - REST에 대해 구체적으로 설명해보세요.

A2 - 자원을 이름(자원의 표현)으로 구분하여 해당 자원의 상태(정보)를 주고 받는 모든 것을 의미합니다. HTTP URI를 통해 자원을 명시하고, HTTP Method를 통해 해당 자원에 대한 CRUD Operation을 적용하는 것입니다.

<br/>

Q3 - 'RESTful'이 무슨 의미인지 아나요?

A3 - REST를 REST 답게 쓰기 위한 방법으로, REST API를 제공하는 웹서비스를 RESTful하다고 합니다. 이해하기 쉽고 사용하기 쉬운 REST API를 만드는 것이 RESTful의 목적입니다.

<br/>

## :page_with_curl: Reference

[[Network] REST란? REST API란? RESTful이란?](https://gmlwjd9405.github.io/2018/09/21/rest-and-restful.html)

[[용어 뜻/설명] REST, RESTful API란?](https://m.blog.naver.com/azure0777/221066646741)

[[Server] Restful API란?](https://mangkyu.tistory.com/46)