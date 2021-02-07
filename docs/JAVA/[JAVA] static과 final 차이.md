# [JAVA] static과 final 차이

:writing_hand: *Assembled by JiYoung-Kwon (2021-02-07)* 



## 1. Static

#### 1-1. static 변수

* static으로 선언된 변수는 **메모리 공간에 하나만 존재** 하며, **어디서나 접근이 가능** 한 변수임

  * 어디서나 접근이 가능하려면 static 변수도 public으로 선언되어야 함

  * 클래스 내부에서는 얼마든지 직접 접근이 가능함

  * 클래스 외부에서 **인스턴스의 이름이나 클래스의 이름을 통해** 접근하는 것도 가능함

    * default 변수일 땐 동일한 패키지로 묶였을 경우

* 한 클래스의 static 변수는 Class영역에 저장되어 있어 어떤 인스턴스든 모두 똑같은 값을 가짐

* **초기화 시점**

  * **인스턴스가 생성되기 이전** 에 별도의 메모리 공간에 할당되어 초기화까지 완료됨
    * 컴파일러에 의해 .java에서 .class 파일로 로드될 시
      * 따라서, 객체가 heap영역 메모리에 올라가기 전에 호출해서 사용할 수 있음
  * 초기화 시점 : JVM(Java Virtual Machine)에 의해 클래스가 메모리 공간에 올라가는 순간
  * **주의**
    * 가비지 컬렉터 관리 밖에 있어 항상 메모리에 상주해 있기 때문에, 프로젝트가 커지고 시스템이 오랜 시간 동안 돌아가게 되면 시스템 운영속도가 점차 느려질 수 있음

* **사용 이유**

  * 인스턴스 간에 **데이터 공유** 가 필요한 상황


<br/>

#### 1-2. static 메소드

* 인스턴스를 생성하지 않아도 static 메소드를 호출할 수 있음
* static 메소드 안에서 외부에 접근하려는 요소 (field, method)들은 모두 static이어야 함
* static 메소드는 super나 this를 사용할 수 없음
* **사용 이유**
  * 객체를 생성할 필요 없는 메소드에 붙여 사용
  * 인스턴스 변수에 접근하지 않는 경우에 메소드로 정의해 사용
* **public static void main**
  - main 메소드는 **인스턴스의 생성과 관계없이 JVM에 의해 호출되므로 반드시 static으로 선언**

<br/>

#### 1-3. static 블록

* 해당 객체가 new를 통해 인스턴스화 될 때 최초 한 번만 호출

* ```java
  public class MyStaticClass {
    static int a = 10;
    static int b;
  
    //static block
    static {
      System.out.println("static block");
      b = a * 4;
    }
  
    public MyStaticClass() {
      System.out.println("new MyStaticClass");
    }
  }
  
  //Main
   public static void main(String [] args) {
     System.out.println("front main");
     System.out.println("a : " + MyStaticClass.a + ", b : " + MyStaticClass.b);
     MyStaticClass myStatic = new MyStaticClass();
   }
  ```

<br/>

#### 1-4. static 중첩 클래스 (내부 클래스)

- 최상위 클래스를 static으로 만들 수 없으나, 클래스를 static으로 만들 수는 있음

- 일반 클래스의 **내부 클래스를 static으로 선언하면 가능**

- 즉, **중첩 클래스에서만 static을 사용할 수 있음**

- ```java
  public class MyNestedClass {
  
    //static class
    public static class NestedStaticClass {
      public static void printStaticMsg() {
        System.out.println("NestedStaticClass");
      }
  
      public void printMsg() {
        System.out.println("NestedStaticClass");
      }
    }
  
    //inner class
    public class InnerClass {
      public void print() {
        System.out.println("InnerClass");
      }
    }
  }
  
  //Main
  public static void main(String [] a) {
    //static 클래스(중첩 클래스)의 static 메소드 접근
    MyNestedClass.NestedStaticClass.printStaticMsg();
  
    //static 클래스(중첩 클래스)생성 후 해당 클래스의 일반 메소드 접근
    MyNestedClass.NestedStaticClass nestedStaticClass = new MyNestedClass.NestedStaticClass();
    nestedStaticClass.printMsg();
  
    //일반 클래스의 내부 클래스 생성 후 메소드 접근
    MyNestedClass.InnerClass innerClass = new MyNestedClass().new InnerClass();
    innerClass.print();
  }
  ```

<br/>

## 2. Final

#### 2-1. final 변수

- 변수를 상수화 시킴

- 즉, 한번 값이 결정된 변수의 값은 **변경이 불가능** 함

- ```java
   final int a;
           //final int a=1; 상수 선언과 함께 값을 정의해도 된다.
  		 Scanner s= new Scanner(System.in);
  		 a=s.nextInt();
           //a=10; 오류 (값을 변경할 수 없다)
  		 System.out.println(a);
  ```

<br/>

#### 2-2. final 클래스

* 클래스를 final로 선언한다면, 이 클래스를 **상속하는 것을 허용하지 않겠다**는 뜻

* 대표적으로 String 클래스가 있음

* ```java
  final class Test{
   int test;
  }
  //class Main extends Child{} final class는 상속할 수 없다.
  //final 키워드를 사용한 Test 클래스는 객체를 생성할 수 없다.
  ```

<br/>

#### 2-3. final 메소드

* 메소드를 final로 선언한다면, 이 메소드의 **오버라이딩을 허용하지 않겠다**는 뜻

* 클래스는 상속이 가능하되 해당 메소드는 오버라이딩이 불가능함

* ```java
  class Test{
  	public final void test2(){
  		//내용정의
  	}
  }
  public class Main extends Test{
  	//public test2(){} compile error: final method는 오버라이딩 못함
  }
  ```

<br/>

## 3. static final

* 클래스 내부 또는 외부에서 참조의 용도로만 선언된 변수는 static final로 선언함
* ex) static final double PI = 3.14;
* 객체(인스턴스)가 아닌 클래스에 존재하는 단 하나의 상수
* 즉, 객체마다 값이 바뀌는 것이 아닌 클래스에 존재하는 상수임 
  - 선언과 동시에 초기화를 해 주어야 함

* 원주율, 산소의 질량 등 **누구나 알고 있는 변하지 않는 상수의 값** 을 static final로 설정하여 변경되지 않도록 함

#### 3-1. final vs static final

- **static final**
  - 선언한 변수를 사용하면 재할당하지 못함
  - 메모리에 한 번 올라가면 같은 값을 클래스 내부의 전체 필드와 메서드에서 공유함
- **final**
  - 선언한 변수를 사용하면 재할당하지 못함
  - 해당 필드, 메서드 별로 호출할 때마다 새로이 값이 할당(인스턴스화)됨
- **상수로 사용하려고 할 때, 그 값은 변하지 않을 것인데 호출할 때마다 새롭게 인스턴스화할 필요가 없기 때문에 static final을 관습적으로 사용함**



## :page_with_curl: Reference

[[JAVA] final 과 static 의 핵심 정리](https://goodncuteman.tistory.com/4)

[[Java] final 과 static final 차이](https://m.blog.naver.com/PostView.nhn?blogId=goddlaek&logNo=220889229659&proxyReferer=https:%2F%2Fwww.google.com%2F)

[[Java]static](https://blog.naver.com/goddlaek/220888359923)

[[Java 기초] static](https://it-mesung.tistory.com/86)

[[Java] 왜 private 상수는 관습적으로 private static final로 선언할까?](https://zorba91.tistory.com/275)