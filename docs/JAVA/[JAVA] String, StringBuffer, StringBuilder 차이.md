# [JAVA] String, StringBuffer, StringBuilder 차이

:writing_hand: *Assembled by JiYoung-Kwon (2021-01-31)* 



#### :pushpin: String, StringBuffer, StringBuilder의 공통점

* String(문자열)을 저장하고 관리하는 클래스들

***



## 1. String

* **String의 특징**

  - 불변의 성질을 가짐

  - StringBuffer, StringBuilder와 다르게 **리터럴을 통해 생성되면 그 인스턴스의 메모리 공간은 절대 변하지 않음**

  - 리터럴로 생성하면 **String Pool** 공간에 생성되며, 문자열 값은 절대 **변하지 않음**

    - '+' 연산, concat() 메서드를 이용하여 변화를 주어도 메모리 공간 내의 값이 변하지 않음
    - String Pool 공간 안에 메모리를 할당 받아 **새로운 String 클래스 객체를 만들어** 문자열을 나타냄

    > 예시
    >
    > ```
    > String s = "ABC";
    > s += "DEF";
    > ```
    >
    > - String 객체는 내부 데이터를 수정할 수 없으므로 "ABCDEF"라는 새로운 객체가 생성되고, data 변수는 이 객체를 참조
    >
    > - 기존에 있던 객체는 참조되지 않게 되어 가비지 컬렉션의 메모리 해제를 기다리게 됨
    >
    >   ![img](https://blog.kakaocdn.net/dn/Y5uyc/btqEa0VABIn/qyBqm9kXuxqWju1HXX83C0/img.png)
  
* **String의 장점**

  - 불변하기 때문에 단순 조회 연산에서는 타 클래스보다 빠르게 읽을 수 있음
  - 불변하기 때문에 멀티쓰레드 환경에서 동기화를 신경 쓸 필요가 없음

  

* **String의 단점**

  - 언제 제거될 지 모름
    - 새로운 문자열이 만들어지면, 기존의 문자열은 가비지 콜렉터에 의해 제거되어야 하기 때문
  - 성능 문제
    - 문자열 연산이 많아질 경우, 계속해서 문자열 객체를 만드는 오버헤드가 발생



* **StringBuffer, StringBuilder와의 차이**
    * String 객체는 한번 생성되면 할당된 공간이 변하지 않음 (불변)
    * 다른 두 클래스의 경우 객체의 공간이 부족해지면 버퍼의 크기를 유연하게 늘려줌 (가변)



  * **String 클래스 사용이 적절한 경우**

      * 문자열 연산이 적고, 자주 참조하는 경우

<br/>

## 2. StringBuffer와 StringBuilder

* **공통적 특징**

  - 크기가 유연하게 변하는 가변적 특성을 가짐
    - 문자열 연산 시 클래스는 한 번만 만들고, 메모리 값을 변경시켜 문자열을 변경함
  - 두 클래스가 제공하는 메서드도 같고, 사용하는 방법도 동일

  

* **장점**
    * 문자열 객체를 계속 만들지 않기 때문에 연산이 잦을 때 사용하면 성능이 좋음
    * 두 클래스의 메서드들이 같아 호환이 가능

  

* **단점**

  * Buffer size를 초기에 설정해야 함

    -> 이 동작으로 인해 String 객체보다 생성 속도가 느리게 됨

  * 문자열 수정 시, 버퍼의 크기를 늘리거나 줄이고 명칭을 변경해야하는 내부적 연산이 필요
    
    * 많은 양의 수정이 아니라면 String 객체가 나을 수 있음

  

* **StringBuffer, StringBuilder가 적절한 경우**
  * 문자열 연산이 많을 때
    * 멀티쓰레드 환경 : StringBuffer
    * 싱글쓰레드 환경 / 멀티쓰레드 환경이지만 동기화가 필요 없는 경우 (1만번 미만의 연산인 경우) : StringBuilder
    * 연산이 많지 않은 경우 : StringBuffer나 StringBuilder나 차이가 거의 없음

<br/>

#### 2-1. StringBuffer vs StringBuilder

  - StringBuffer : Thread-safe함

      - 멀티쓰레드 환경에서 synchronized 키워드를 사용할 수 있어 멀티쓰레드 상태에서 동기화를 지원

        > Thread-safe : 멀티쓰레드 프로그래밍에서 일반적으로 어떤 함수나 변수, 혹은 객체가 여러 스레드로부터 동시에 접근이 이루어져도 프로그램 실행에 문제가 없음을 뜻함

    - StringBuffer 예제

      ```java
      public class StringBuffer_Ex{
          public static void main(String[] args){
              String s = "abcdefg";
              StringBuffer sb = new StringBuffer(s);
              
              System.out.println("처음 상태 : " + sb); // 처음 상태 : abcdefg
              System.out.println("문자열 String 반환 : " + sb.toString()); // String 변환 : abcdefg
              System.out.println("문자열 추출 : " + sb.substring(2, 4)); // 문자열 추출 : cd
              System.out.println("문자열 추가 : " + sb.insert(2, "추가")); // 문자열 추가 : ab추가cdefg
              System.out.println("문자열 삭제 : " + sb.delete(2, 4)); // 문자열 삭제 : abcdefg
              System.out.println("문자열 연결 : " + sb.append("hijk")); // 문자열 연결 : abcdefghijk
              System.out.println("문자열의 길이 : " + sb.length()); // 문자열 길이 : 11
              System.out.println("용량의 크기 : " + sb.capacity()); // 용량의 크기 : 23
              System.out.println("문자열 역순 변경 : " + sb.reverse()); // 문자열 역순 변경 : kjihgfedcba
              System.out.println("마지막 상태 : " + sb); // 마지막 상태 : kjihgfedcba
          }
      }
      ```

  - StringBuilder : Thread-safe 하지 않음

      - 동기화를 지원하지 않기 때문에 멀티쓰레드 환경에 적합하지 않음
    - 대신, StringBuffer에 비해 싱글쓰레드 환경에서 연산처리가 빠름

  - StringBuilder가 StringBuffer 보다 속도는 빠르지만, 현업에서는 언제 멀티쓰레드 환경에서 돌아갈지 알 수 없어, 안정적인 StringBuffer를 사용하기도 함

<br/>


## :bulb: 예상질문

Q1 - String과 StringBuffer & StringBuilder의 차이는 무엇인가요?

A1 - String 객체는 불변이어서 한번 생성되면 할당된 공간이 변하지 않습니다. 다른 두 클래스의 경우 가변으로, 객체의 공간이 부족해지면 버퍼의 크기를 유연하게 늘려줍니다.

<br/>

Q2 - StringBuffer과 StringBuilder의 차이가 무엇인가요?

A2 - StringBuffer는 synchronized 키워드를 사용할 수 있어 동기화를 지원하여 Thread-safe합니다. 따라서 멀티쓰레드 환경에 적합합니다. 그에 비해 StringBuilder은 동기화를 제공하지 않기 때문에 Thread-safe하지 않지만, StringBuffer에 비해 싱글쓰레드 환경에서 연산처리가 빠릅니다.

<br/>

## :page_with_curl: Reference

[JAVA String, StringBuffer, StringBuilder 차이점](https://jeong-pro.tistory.com/85)

[[Java] String, StringBuffer, StringBuilder의 차이점과 사용이유](https://coding-factory.tistory.com/546)

[Java StringBuffer vs StringBuilder 차이 (간단 예제 코드)](https://gofnrk.tistory.com/83)

[[OS] Thread Safe란?](https://gompangs.tistory.com/entry/OS-Thread-Safe란)