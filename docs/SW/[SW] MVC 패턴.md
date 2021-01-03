# [SW] MVC 패턴

:writing_hand: *Assembled by JiYoung-Kwon (2020-12-30)* 



## 1. MVC 패턴이란?

**MVC** - Model, View, Controller의 약자로 소프트웨어 공학에서 사용되는 소프트웨어 **디자인 패턴**

![img](https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/327/1262.png) 

> * 사용자가 **Controller**를 조작하면 Controller는 **Model**을 통해서 데이터를 가져오고, 그 정보를 바탕으로 시각적인 표현을 담당하는 **View**를 제어해서 사용자에게 전달하게 된다.
> * **디자인 패턴** : 건축으로치면 공법에 해당하는 것으로 소프트웨어의 개발 방법을 **공식화**한 것. 소수의 뛰어난 엔지니어가 해결한 문제를 다수의 엔지니어들이 처리할 수 있도록 한 규칙, 구현자들 간의 커뮤니케이션의 효율성을 높이는 기법  [<참고 : Wikipedia>](https://ko.wikipedia.org/wiki/%EB%94%94%EC%9E%90%EC%9D%B8_%ED%8C%A8%ED%84%B4)

* **Model** : 백그라운드에서 동작하는 로직 처리

* **View** : 사용자가 보게될 결과 화면 출력

* **Controller** : 사용자의 입력처리와 흐름 제어 담당

**MVC pattern**은 이렇게 도메인(비즈니스) 로직과 UI 로직을 분리하여 유지보수를 독립적으로 수행할 수 있게 하는 장점이 있다.



## 2. WEB과 MVC

WEB에 적용된 MVC 예시

1. 사용자가 웹 사이트에 접속 (Uses)
2. Controller는 사용자가 요청한 웹 페이지를 서비스 하기 위해 Model을 호출 (Manipulates)
3. Model은 DB나 파일과 같은 데이터 소스를 제어한 후, 그 결과를 리턴함
4. Controller는 Model이 리턴한 결과를 View에 반영 (Updates)
5. 데이터가 반영된 View는 사용자에게 보여짐 (Sees)



## 3. 구성

#### 3-1. Model ​

* Model, Domain

* 프로그램이 목표하는 작업을 원활하게 수행하기 위해 필요한 물리적 개체, 규칙, 작업 등의 요소들을 구분되는 역할로써 정의해놓은 것

* DTO, DAO로 분류할 수 있음

* 데이터를 가진 객체, 파라미터로 주로 쓰임

* DB의 테이블과 대응하는 경우가 많다. 

***

#### 3-2. View

* 사용자가 보는 화면에 입출력 과정 및 결과를 보여주기 위한 역할을 함

* 객체를 전달받아 상태를 바로 출력하는 역할만을 담당 *(도메인 로직의 어떤 것도 알고 있으면 안됨)*

* View에서는 도메인 객체의 상태를 따로 저장하고 관리하는 클래스 변수 / 인스턴스 변수가 있을 필요가 없다.

***

#### 3-3. Controller

* model과 view를 연결시켜주는 다리 역할

* 도메인 객체들의 조합을 통해 프로그램의 작동 순서나 방식을 제어

* 사용자가 접근한 URL에 따라 사용자 요청사항을 파악한 후, 그 요청에 맞는 데이터를 Model에 의뢰하고, 데이터를 View에 반영해 사용자에게 알려준다.

  

## 4. Model 1과 Model 2

#### 4-1. Model 1

* 비즈니스 로직 영역(Controller)에 프레젠테이션 영역(View)를 같이 구현하는 방식

* 사용자의 요청을 JSP가 전부 다 처리

* ![img](https://blog.kakaocdn.net/dn/6SIUm/btqzYCsgeQE/IYkMcagYXWwMf7NSbRFJu0/img.png)

  * 장점 : 빠르고 쉽게 개발할 수 있음

  * 단점 : JSP 파일 자체가 너무 비대해짐, 향후 유지보수에 어려움을 겪을수 있음

***


#### 4-2. Model 2

* 비즈니스 로직 영역과 프레젠테이션 영역이 분리되어 있는 구현 방식

* 웹 브라우저 사용자의 요청을 Servlet이 받음

* Servlet은 요청을 View로 보여줄 것인지, Model로 보내줄 것인지 정하여 전송

* View는 보여주는 역할만 담당, 실질적인 기능의 부분은 Model에서 담당

* ![img](https://blog.kakaocdn.net/dn/GSBZ4/btqzZdec5re/4LYL59sQl6B72Ak4tlknP0/img.png)

  * 장점 : View와 Controller 분리 -> 디자이너와 개발자의 분업이 가능, 유지보수 유리
  * 단점 : 설계에서 어려움을 겪을 수 있고, 개발 난이도가 높음



## 5. 장ㆍ단점

#### 5-1. 장점

* 서로 분리되어 전체적인 구조에서 분업을 만들어 낼 수 있음

* 유지보수성, 애플리케이션의 확장성, 유연성 증가

* 중복코딩의 문제점이 사라질 수 있음

#### 5-2. 단점

* View와 Model이 서로 의존성을 띄게 되어 구조가 복잡해질 수 있음
  * 한 Model은 다수의 View를 가질 수 있고 반대로 Controller를 통해 한 View에 연결되는 Model도 여러개가 될 수 있음 -> 이런 관계는 View와 Model의 의존성을 높이게 됨
  
  * Controller에 다수의 Model과 View가 연결되는 복잡한 상황이 유발 되는 상황이 생길 수 있음
  
  * MVC 규모가 복잡하고 비대해져, 새 기능을 추가할 때마다 의존성을 일일이 해결해야 하는 상황이 오게 됨 
  
  * **Massive View Controller**  *( MVC의 한계를 표현하는 용어 )*
  
    

## :page_with_curl: Reference

* [[MVC 패턴이란?] (Model 1, Model 2)](https://wooaoe.tistory.com/15)

* [MVC 디자인 패턴](https://opentutorials.org/course/697/3828)

* [MVC 패턴](https://velog.io/@ljinsk3/MVC-%ED%8C%A8%ED%84%B4)