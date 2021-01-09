# [SW] 프로그래밍 패러다임

:writing_hand: *Assembled by JiYoung-Kwon (2021-01-03)* 



## 1. 프로그래밍 패러다임*(Programming Paradigm)*이란?

#### 1-1. 프로그래밍

  * 프로그래밍 언어로 컴퓨터 프로그램을 작성하는 일, 코딩(coding)

#### 1-2. 패러다임

* (세계를) 이해하는 방식, 즉 인식틀

#### 1-3. 프로그래밍 패러다임

* 프로그래밍을 구성하는 요소들을 어떤 관점으로 보고 이해하는가
* 프로그램을 작성할 때의 관점 내지 방법론
* ""프로그래밍 언어는 OO 패러다임을 갖는다."
* 여러 패러다임을 갖는 언어 = 멀티 패러다임 언어



## 2. 종류

![image-20210104231145100](https://user-images.githubusercontent.com/45457678/83468305-54638480-a4b7-11ea-9041-2da165d53b3e.png)

[<Wikipedia 참고>](https://ko.wikipedia.org/wiki/%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D_%ED%8C%A8%EB%9F%AC%EB%8B%A4%EC%9E%84)



#### 2-1. 명령형 프로그래밍 (imperative programming)

* 선언형 프로그래밍과 반대되는 개념
* 알고리즘을 명시하지만 목표는 명시하지 않는다.
* `어떻게(How)`
* 코드로 원하는 결과를 달성해 나가는 과정에만 관심을 둠

***

##### :book: POP

* **Procedural Oriented Programming**의 줄임말로, 절차 지향 프로그래밍이라고 부른다.

* 순서대로 명령을 받아 문제를 해결하는 방식 (**순차적인 처리**)

* 대표적인 절차지향 언어 : C언어

* 장점

  > 1. 가장 직관적이다.
  > 2. 실행처리 속도가 빠르다.

* 단점

  > 1. 유지보수가 어렵다.
  > 2. 정해진 순서대로 입력을 해야되므로 순서가 바뀌면 결과값을 도출하기 어렵다.
  > 3. 프로그램을 분석하기 어렵다.
  > 4. 대형 프로젝트에는 부적합하다.

***

##### :book: OOP :star:

* **Object Oriented Programming**의 줄임말로, 객체 지향 프로그래밍이라고 부른다.

* 프로그램을 작게 나누고, 그 각각의 단순한 기능을 모아 문제를 해결하는 방식 (**객체들의 모임**)

* 대표적인 객체지향 언어 : JAVA

* 장점

  > 1. 다른 클래스를 가져와 사용할 수 있고, 상속 받을 수 있어 코드의 재사용성 증가
  > 2. 절차지향보다 유지보수가 간단
  > 3. 클래스 단위로 모듈화가 가능하며, 대형 프로젝트에 적합

* 단점

  > 1. 처리 속도가 상대적으로 느리다.
  > 2. 객체가 많으면 용량이 커진다.
  > 3. 설계시 많은 노력과 시간이 필요하다.

***



#### 2-2. 선언형 프로그래밍 (declarative programming)

* 목표는 명시하지만 알고리즘은 명시하지 않는다.
* `무엇을(What)`
* 과정을 하나하나 기술하는 것 보다 필요한 것이 어떤 것인지 기술하는 데 방점을 두고 애플리케이션의 구조를 세워나감
* +ex) DB : Create Table

***

##### :book: FP 

* **Functional Programming**의 줄임말로, 함수형 프로그래밍이라고 부른다.

* 프로그램을 하나의 큰 **함수**로 보고, 그것을 작은 함수들의 합성함수로 구현해 문제를 해결하는 방식

* 대표적인 함수형 프로그래밍 언어 : Scala

  +)1. **장점**

  - 함수가 사이드 이펙트를 가지지 않아 동시성과 관련된 문제를 원천적으로 봉쇄
    - +) 함수에 들어온 input에 대해서만 조작을 해서 output하는 것을 지향함 
  - 테스트 용이

  2. **단점**

  - 상태가 없으므로 함수형 프로그래밍 패러다임만 사용하여 프로그램을 작성할 수 없음

  +) 명령형 -> 함수형 프로그래밍

  ``` javascript
  // 명령형
  function add (arr) {
    let result = 0
    for (let i = 0; i < arr.length; i++){
      result += arr[i]
    }
    return result
  }
  ```

   ```javascript
  // 함수형
  function add (arr) {
    return arr.reduce((prev, current) => prev + current, 0)
  }
   ```

  

##### :book: RP :star:

* **Reactive Programming**의 줄임말로, 반응형 프로그래밍이라고 부른다. 
* **비동기 데이터 흐름**에 기반을 둔 프로그래밍 패러다임
* 언제 변할지 모르는 수많은 데이터를 일일히 추적하기 때문에, 컴퓨터 성능을 저하시켜 고속처리에 사용하기에는 적합하지 않음
* 다수의 비동기 이벤트를 효과적으로 처리할 수 있기 때문에 사용자 경험을 개선할 수 있음

+) 반응형 프로그래밍 장.단점

​	**장점** : 동기식 비효율처리로 인한 병목 현상 해결, 생산성 

​	**단점** : 수많은 데이터를 일일히 추적, 컴퓨터 성능 저하 -> 고속처리에 적합하지 않음

* 반응형이 아닌 경우 : 1초 처리 + 10초 처리 각각이 모여야 View를 그릴 수 있을 경우 => 10초가 걸림
* 반응형 : 따로 요청을 보내서 처리가 끝난 것부터 먼저 그려짐 

![image-20210110063631410](https://github.com/JiYoung-Kwon/Tech-Stack-for-Developer/tree/main/resources/RP.png)

## :page_with_curl: Reference

[프로그래밍 패러다임이란](https://developer.qustory.com/post/programming-paradigm/)

[프로그래밍 언어 패러다임 3가지](https://velog.io/@dnjscksdn98/%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D-%EC%96%B8%EC%96%B4-%ED%8C%A8%EB%9F%AC%EB%8B%A4%EC%9E%84-3%EA%B0%80%EC%A7%80)

[프로그래밍 패러다임](https://daeun28.github.io/%EC%BB%B4%ED%93%A8%ED%84%B0%EA%B3%B5%ED%95%99-%EC%8A%A4%ED%84%B0%EB%94%94/post23/)

