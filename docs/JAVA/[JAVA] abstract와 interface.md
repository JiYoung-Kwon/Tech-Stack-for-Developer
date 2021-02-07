# [JAVA] abstract와 interface

:writing_hand: *Assembled by JiYoung-Kwon (2021-02-07)* 



### :pushpin: 추상 클래스와 인터페이스

* 상속받는 클래스 혹은 구현하는 인터페이스 안에 있는 추상 메소드를 구현하도록 강제함

---

<br/>

## 1. 추상 클래스(abstract)

- 미완성된 클래스
- 클래스 구현부 내부에 **추상 메소드가 하나 이상 포함되거나 abstract로 정의된 클래스**

  - 이 말은 일반 메서드의 구현도 가능하다는 뜻
  - **추상 메서드**
    - 메서드의 선언부만 작성하고 구현부는 미완성인 채로 남겨져 있는 메서드
    - 미완성으로 남겨놓은 이유
      - 상속받는 클래스에 따라 메서드의 내용이 달라질 수 있기 때문
- 클래스의 프레임만 구성되어 있음
- 직접 객체 생성이 불가능함

  - 즉, 인스턴스를 생성할 수 없음
- 추상 클래스에서 정의된 추상적인 기능은 하위 클래스에서 상세 구현함

<br/>


#### 1-1. 목적

  - 동일한 부모를 가지는 클래스를 묶는 개념으로 **상속을 받아서 기능을 이용하고, 확장시키는 것**
  - 새로운 클래스를 작성하는데 있어 그 바탕이 되는 부모 클래스로서 중요한 의미를 가짐

<br/>

#### 1-2. 추상 클래스 상속

* 단일 상속만 가능

* ex)

  * ```java
    package first;
    
    //Animal 추상 클래스
    public abstract class Animal{
        public abstract void sound();
    }
    
    //Animal 추상 클래스를 상속받는 Dog, Cat 클래스
    public class Dog extends Animal{
        public void sound(){
            System.out.println("멍멍");
        }
    }
    
    public class Cat extends Animal{
        public void sound(){
            System.out.println("야옹야옹");
        }
    }
    
    //선언 후, 메인 메소드에서 실행
    public class Main{
        public static void main(String[] args){
            //인스턴스화
            Dog dog = new Dog();
            Cat cat = new Cat();
            
            dog.sound();
            cat.sound();
        }
    }
    ```

* 추상 클래스를 상속 받는 클래스는 추상 클래스에서 선언했던 추상 메서드를 반드시 구현해야 함, 그렇지 않으면 에러가 발생

<br/>

## 2. 인터페이스(interface)

- 밑 그림만 있는 기본 설계도 즉, 뼈대
- 추상 클래스보다 한 단계 더 추상화 되었다고 볼 수 있음
  - 안의 **모든 메서드가 추상 메서드**로 되어있음
  - 자바8에서는 default 키워드를 이용해서 일반 메소드의 구현도 가능은 함
- 추상 클래스와 마찬가지로 직접 객체 생성이 불가능
- 미리 정해진 규칙에 맞게 구현하도록 표준을 제시하는데 사용
- 인터페이스끼리 다중 상속 가능

<br/>

#### 2-1. 목적

* 함수의 구현을 강제화하여, **구현 객체가 같은 동작을 한다는 것** 을 보장하는 것

<br/>

#### 2-2. 제약사항

* 모든 멤버변수는 **public static final** 이어야 함. 단, 생략 가능
* 모든 메소드는 **public abstract** 이어야 함. 단, 생략 가능
  * static 메소드와 default 메소드는 제외 (java 8 이후)

<br/>

#### 2-3. 인터페이스 상속

* 다중 상속 가능

* ex)

  * ```java
    interface Changeable{
        /* 채널을 바꾸는 기능의 메서드*/
        void change(Channel c);
    }
    
    interface Powerable{
         /* 전원을 껐다 켰다하는 메서드*/
        void power(boolean b);
    }
    
    interface Controlable extends Changeable, Powerable{} //다중상속 가능
    ```

    * 부모 인터페이스(Changeable, Powerable)을 모두 상속받는 자식 인터페이스(Controlable)
    * Controlable 안에 정의된 멤버는 하나도 없지만 부모로부터 상속받은 추상메서드 change, power를 멤버로 갖게 됨

  * ```java
    class 클래스이름 implements 인터페이스이름 {
    	// 인터페이스에 정의된 추상메서드를 구현해야 함
    }
    
    class Control implements Controlable{
        public void change(Channel c){/* 내용생략 */}
        public void power(boolean b){/* 내용생략 */}
    }
    ```

    * Controlable 인터페이스를 구현하는 Control 클래스
    * 만일 구현하는 인터페이스의 메서드 중 일부만 구현한다면 abstract를 붙여 추상클래스로 선언해야 함

  * ```java
    class Control extends Channel implements Controlable{
    	public void change(Channel c){/* 내용생략 */}
        public void power(boolean b){/* 내용생략 */}
    }
    ```

    * 상속과 구현을 동시에 할 수도 있음

<br/>

#### 2-4. 장점

**1. 개발시간을 단축시킬 수 있다.**

- 일단 인터페이스가 작성되면, 이를 사용하여 프로그램을 작성하는 것이 가능함
  - 인터페이스가 공통이므로 동시 개발 가능

**2. 표준화가 가능하다.**

- 프로젝트에 사용되는 기본 틀을 인터페이스로 작성한 후 개발되도록 함
- 일관되고 정형화된 프로그램 개발 가능

**3. 서로 관계없는 클래스들에게 관계를 맺어 줄 수 있다.**

- 하나의 인터페이스를 공통적으로 구현함으로써 관계 매핑

**4. 독립적인 프로그래밍이 가능하다.**

- 클래스의 *선언과 구현을 분리* 시킬 수 있음

- 클래스와 클래스 간의 직접적인 관계를 인터페이스를 이용해서 간접적인 관계로 변경하면, 한 클래스의 변경이 관련된 다른 클래스에 영향을 미치지 않는 독립적인 프로그래밍이 가능함

- ex)

  - ![img](https://user-images.githubusercontent.com/58902042/106575411-671ae580-657f-11eb-9f26-535511b448ae.PNG)

  - 실행 결과 : `methodB()`

  - 위의 코드와 같이 Class A와 Class B가 있다고 할 때, Class A는 Class B의 인스턴스를 생성하고 메서드를 호출함

    ![img](https://user-images.githubusercontent.com/58902042/106576131-2b345000-6580-11eb-9475-807d4e8b6ca9.PNG)

  - 이 두 클래스는 서로 직접적인 관계를 가지게 됨

  - Class A를 작성하려면 Class B가 이미 작성되어 있어야 하고, Class B의 methodB()의 선언부가 변경되면 이를 사용하는 Class A도 변경되어야하는 단점이 있음

  <br/>

  * ![img](https://user-images.githubusercontent.com/58902042/106575510-844fb400-657f-11eb-95e9-cc738b764efe.PNG)

  * 실행 결과 : `methodB() in Bclass`

  * 이때 위와 같이 인터페이스를 매개체로 해서 Class A가 인터페이스를 통해 Class B의 메서드에 접근하도록 만들면, Class B가 변경되거나 다른 클래스로 대체되어도 Class A는 전형 영향을 받지 않음

    ![img](https://user-images.githubusercontent.com/58902042/106576615-b57cb400-6580-11eb-9c7c-f3f9335173c8.PNG)

  * 이제 Class A가 Class B를 사용하지 않음

  * 따라서 인터페이스를 통해서만 연결되는 간접적인 관계로 바뀜

    ![img](https://user-images.githubusercontent.com/58902042/106576618-b6ade100-6580-11eb-9f38-3dd57212d0ca.PNG)

  - Interface I는 실제 구현 내용을 감싸고 있는 껍데기이며, Class A는 껍데기 안에 어떤 알맹이(Class)가 있는지 몰라도 됨


<br/>

## 3. 클래스와 인터페이스 사이 관계

[![img](https://user-images.githubusercontent.com/58902042/106485793-540f0380-64f4-11eb-83c0-dfc8166cbc6e.PNG)](https://user-images.githubusercontent.com/58902042/106485793-540f0380-64f4-11eb-83c0-dfc8166cbc6e.PNG)

- **extends** : 같은 클래스, 인터페이스끼리 상속 받을 때
- **implements** : 클래스가 인터페이스를 구현 할 때
- 인터페이스는 인터페이스로만 상속 받을 수 있음

<br/>

## 4. 추상 클래스 vs 인터페이스

* **공통점**
  * 선언만 있고 구현 내용은 없는 클래스
  * 인스턴스화 할 수 없음
  * 추상클래스를 extends로 상속받은 자식들과 인터페이스를 implements하고 구현한 자식들만 객체를 생성할 수 있음
    - 즉, 자식들이 반드시 무언가를 구현하도록 위임할 때 사용됨
* **차이점**
  * 인터페이스는 클래스가 아니지만 추상 클래스는 클래스임
  * 인터페이스는 다중상속이 가능하고, 추상 클래스는 단일상속만 함
  * 추상클래스는 상속을 받아 기능을 확장 즉, 부모의 유전자를 물려받음(IS-A)
  * 인터페이스는 구현하는 모든 클래스에 대해 특정한 메서드가 반드시 존재하도록 강제하는 역할을 함. 유전자가 아니라 사교적으로 필요에 따라 결합하는 관계라는 뜻(HAS-A)

|   구분    | 추상 클래스                                                  | 인터페이스                                                   |
| :-------: | ------------------------------------------------------------ | ------------------------------------------------------------ |
|   선언    | abstract class 클래스명 { 변수; 메서드() {...} abstract 메서드(); } | interface 인터페이스명 { 상수; // public final static 메서드(); // public abstract } |
| 상속구현  | class Sub **extends** super { 메서드 재정의 // overriding }  | class Sub **implements** Interface1, Interface2 { 메서드 재정의 // overriding } |
| 상속 특징 | 단일 상속                                                    | 다중 상속                                                    |

<br/>

## :page_with_curl: Reference

[추상클래스와 인터페이스의 차이가 뭐죠?](https://cbw1030.tistory.com/47)

[[Java\] 추상 클래스(abstract class)와 인터페이스(interface)](https://you9010.tistory.com/155)

[[[Java\] 추상 클래스(Abstract class)와 인터페이스(Interface)](https://pridiot.tistory.com/50)

[인터페이스(interface)와 추상 클래스(abstract class)](https://loustler.io/languages/oop_interface_and_abstract_class/)

[자바의 추상 클래스와 인터페이스](https://brunch.co.kr/@kd4/6)