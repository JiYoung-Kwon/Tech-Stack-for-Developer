# [JAVA] 자바 업캐스팅 다운캐스팅

:writing_hand: *Assembled by JiYoung-Kwon (2021-01-24)* 



#### :pushpin: 캐스팅이란?

* 타입을 변환하는 것

* **형변환**이라고도 함

* 자바의 상속 관계에 있는 부모와 자식 클래스 간에는 서로 간의 형변환이 가능

* OOP(객체지향프로그래밍)에서 매우 중요함

  * OOP의 다형성과 관련이 있기 때문

  * 데이터를 바꾸는 것이 주 목적이 아닌, 다형성 측면에서 사용함

  * ```java
    //컴파일 에러 - 실제 데이터 1.0이 1로 바뀌기 때문에 실제 데이터가 손실되는 것을 막고자 하는 것
    int a = 1.0;
    
    //프로그래머가 데이터가 손실된다는 것을 이미 알고 있고, OOP의 다형성을 이용하고 싶을 때 캐스팅
    int a = (int)1.0;
    
    //반대 상황 - 컴파일 에러가 뜨지 않음 (기본형끼리의 캐스팅이기 때문)
    double b = 1; 
    ```

* 서로 관련없는 데이터끼리는 변환되지 않음 `int a = (int)true;`

* 참조형 데이터가 관련있는 경우

  1. 상속 관계가 맺어진 경우
  2. 인터페이스로 인해 확장이 된 경우

***





## 1. 업 캐스팅(Upcasting)

* **서브 클래스의 객체가 수퍼 클래스 타입으로 형변환 되는 것**

* 서브 클래스는 수퍼 클래스의 모든 것을 상속 받음

  -> 서브 클래스는 수퍼 클래스로 취급 될 수 있음

* 즉, 수퍼 클래스 레퍼런스 변수가 서브 클래스로 객체화된 인스턴스를 가리킬 수 있게 됨

* 예시 코드

  ```java
  class Person {
      String name;
  
      public Person(String name) {
          this.name = name;
      }
  }
  
  class Student extends Person {
      String dept;
  
      public Student(String name) {
          super(name);
      }
  }
  
  public class CastingTest {
      public static void main(String[] args) {
          // 레퍼런스 student를 이용하면 name, dept에 접근 가능
          Student student = new Student("JJIYOM");
  
          // 레퍼런스 person을 이용하면 Student 객체의 멤버 중
          // 오직 Person 클래스의 멤버만 접근이 가능
          Person person = student;
          person.name = "KwonJiYoung";
          
          // 아래 문장은 컴파일 타임 오류
          //dept 멤버는 Student 타입의 멤버이므로
          person.dept = "Computer Eng";
      }
  }
  ```

  * 업캐스팅을 하게 되면 객체 내에 있는 모든 멤버에 접근할 수 없음
    * 오직 수퍼 클래스의 멤버에만 접근이 가능함
    * 멤버 필드뿐만 아니라 메서드에도 동일하게 적용됨

* 업캐스팅 시에는 명시적인 타입 캐스팅 선언을 **하지 않아도 됨**

  * 변수가 원하는 정보를 인스턴스가 모두 가지고 있으므로 (Student 클래스는 Person 클래스를 상속받았기 때문) 컴파일러가 형변환 기호를 붙이지 않더라도 다형성 측면에서 넘어감

  ```java
  // 업캐스팅 자동 타입 변환
  Person person = student;
  
  // 아래와 같이 명시적으로 타입 캐스팅 선언을 하지 않아도 된다.
  Person person = (Person) student;
  ```

  

## 2. 다운 캐스팅(Downcasting)

* **자신의 고유한 특성을 잃은 서브 클래스의 객체를 다시 복구 시켜주는 것**

* 업캐스팅 된 것을 다시 원상태로 돌리는 것

* 예시 코드

  ```java
  class Person {
      String name;
  
      public Person(String name) {
          this.name = name;
      }
  }
  
  class Student extends Person {
      String dept;
  
      public Student(String name) {
          super(name);
      }
  }
  
  public class CastingTest {
      public static void main(String[] args) {
          // 업캐스팅 선행
          Person person = new Student("JJIYOM");
  
          // 다운캐스팅
          Student student = (Student) person;
  
          // Okay!
          student.name = "KwonJiYoung";
  
          // Okay!
          student.dept = "Computer Eng";
      }
  }
  ```

* **명시적으로** 타입을 지정해야 함

  * Student 클래스가 Person 클래스를 상속 받았기 때문에 더 많은 데이터를 가지고 있을 것
  * 지정 X 시, **컴파일 오류** 발생

* 업캐스팅이 **선행**이 되어야 함

* 무분별한 다운캐스팅은 컴파일 시점에는 오류가 발생하지 않아도 **런타임 오류**를 발생시킬 가능성이 있음

  ```java
  Student student = (Student) new Person("JJIYOM");
  ```

  * 형변환할 타입을 명시함으로서 컴파일 오류는 사라졌지만, 실제 코드를 수행하면서 ClassCastException이 발생할 수 있음
    * ClassCastException : 어느 객체를 상속 관계에 없는 클래스에 캐스트하려고 할 때 발생
    * Student 데이터가 무엇인지 모르기 때문 (JVM이 추리하지 못함)

* 이렇게 혼동되는 객체를 구별하기 위해 도움을 주는 연산자 : instanceof

<br/>

## 3. instanceof

* 객체 타입을 구분하기 위해 instanceof 연산자를 사용

* 형태 : [객체 레퍼런스] instanceof [클래스 타입]

* 결과 값 : boolean 타입으로 true, false를 반환 값으로 가짐

* 사용시 주의할 점

  * instanceof 연산자는 객체에 대한 클래스(참조형) 타입에만 사용할 수 있음

* 예시

  * 클래스 계층 구조

    <img src = https://blog.kakaocdn.net/dn/SdIVj/btqx8zC7SMx/RuUECGwzUuzFNSmfTii591/img.png width = 50%>

  * 코드

    ```java
    Person jee = new Student();
    Person kim = new Professor();
    Person lee = new Researcher();
    
    if(jee instanceof Person)		//jee는 Person타입을 상속 받았음으로 true
    if(jee instanceof Student)		//jee는 Student타입이므로 true
    if(kim instanceof Student)		//kim은 Student타입이 아니므로 false
    if(kim instanceof Professor)	//kim은 Professor타입이므로 true
    if(kim instanceof Researcher)	//kim은 Researcher타입을 상속 받았음으로 true
    if(lee instanceof Professor)	//lee는 Professor타입이 아니므로 false
    if("java" instanceof String)	//"Java"는 String 타입의 인스턴스이므로 true;
    if(3 instanceof int)			//문법 오류. instanceof는 객체에 대한 레퍼런스에만 사용
    ```

<br/>

## :bulb: 예상질문

Q1 - 업캐스팅이란 무엇인가요?

A1 - 서브 클래스의 객체가 수퍼 클래스 타입으로 형변환되는 것입니다. 명시적인 타입 캐스팅 선언을 하지 않아도 됩니다.

<br/>

Q2 - 다운캐스팅이란 무엇인가요?

A2 - 업캐스팅된 것을 다시 원 상태로 돌리는 것으로, 업캐스팅이 선행되어야 하고 명시적으로 캐스팅 타입을 지정해주어야 합니다. 무분별한 다운캐스팅은 컴파일 오류가 발생하지 않아도 런타임 오류를 발생시킬 가능성이 있기 때문에 주의해야 합니다.

<br/>

Q3 - instanceof에 대해 아나요?

A3 - instanceof는 자바에서 객체 타입을 구분할 수 있는 기능을 제공하는 연산자입니다. boolean 타입으로 true와 false값을 가지고 있습니다. 이 연산자는 참조형(객체에 대한 클래스) 타입에만 사용할 수 있습니다.

<br/>

## :page_with_curl: Reference

[JAVA - Casting(캐스팅)](https://mommoo.tistory.com/40)

[JAVA - UpCasting(업캐스팅)](https://mommoo.tistory.com/41)

[JAVA - DownCasting(다운캐스팅)](https://mommoo.tistory.com/51)

[[JAVA] 15.업캐스팅, 다운캐스팅, instanceof](https://lbmmbl.tistory.com/29)

[자바 업캐스팅 다운캐스팅](https://madplay.github.io/post/java-upcasting-and-downcasting)