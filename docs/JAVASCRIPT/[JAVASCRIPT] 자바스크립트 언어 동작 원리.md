# [JAVASCRIPT] 자바스크립트 언어 동작 원리

:writing_hand: *Assembled by JiYoung-Kwon (2021-01-16)* 



## 1. 자바스크립트

- JavaScript는 싱글 스레드, 논-블로킹 언어

- **싱글 스레드**

  - 하나의 힙 영역과 하나의 콜 스택을 가짐
  - 한 번에 한 가지 일 밖에 하지 못한다는 의미

- **콜 스택**

  - 함수가 실행되는 순서를 기억하고 있음

  - 함수를 실행하려면 스택의 가장 위에 해당 함수를 넣게 되고, 함수에서 리턴이 일어나면 스택의 가장 위쪽에서 함수를 꺼냄

  - 스택 프레임(Stack Frame) : 호출 스택의 각 단계

  - 예제

    <img src = https://beomy.github.io/assets/img/posts/javascript/call_stack.gif width = 80%>

  - 콜 스택 에러 메시지

    ![에러 콜 스택](https://beomy.github.io/assets/img/posts/javascript/error_call_stack.png)

  - 스택 오버플로우

    ![Image for post](https://miro.medium.com/max/521/1*MkZ3Kb667QeE4xKCtio_rA.png)

    * 스택의 사이즈르 초과했을 때 발생하는 오류
    * 재귀를 잘못 구현했을 때 쉽게 마주할 수 있는 오류

- **논-블로킹**

  * 블로킹

    * 콜 스택이 멈춘 상태

    * 사용자 화면의 버튼을 클릭해도 반응이 없는, 사용자와 인터랙션(interaction) 할 수 없는 상태가 됨

      <img src = https://beomy.github.io/assets/img/posts/javascript/blocking.png width = 50%>

    * 해결 방법 : 논-블로킹, 비동기 콜백을 사용하는 것

  * 통신이 완료될 때까지 기다리지 않고, 다른 작업을 수행할 수 있음



## 2. 자바스크립트 엔진

* JavaScript로 작성한 코드를 해석하고 실행하는 인터프리터
* 대표적인 예 : Google V8 엔진 (Chrome과 Node.js에서 사용)

![Image for post](https://miro.medium.com/max/2358/1*i48z012J7T2eO1Hbl3mgpg.png)

* 대부분의 JavaSciprt Engine은 Call Stack, Task Queue(Event Queue), Heap이라는 세 가지 영역으로 구분됨

* 추가적으로 Event Loop으로 Task Queue의 task들을 관리할 수 있음

  * **Memory Heap** : 메모리 할당이 일어나는 곳

    * 동적으로 생성된 객체(인스턴스)가 할당되는 곳

    * 동적으로 할당되는 변수의 경우, 컴파일러는 얼마나 많은 메모리를 필요로 할 지 알 수 없음 

      -> 컴파일러는 스택에 변수를 위한 공간을 할당할 수 없음

      -> 동적 변수를 런타임 시점에 Heap공간에 할당받음

  * **Call Stack** : 코드 스택에 따라 호출 스택이 쌓이는 곳

  * **Task Queue(Event Queue)** : 런타임 환경에서 처리해야 하는 Task를 임시로 저장하는 대기 Queue



## 3. 자바스크립트 런타임

<img src = https://joshua1988.github.io/images/posts/web/translation/how-js-works/js-engine-runtime.png width = 80%>

* Call Stack에서 실행된 비동기 함수는 Web API를 호출

* Web API는 (이벤트 발생 시 실행 할) 콜백함수를 Callback Queue에 순차적으로 적재

* Callback Queue에 적재된 함수들은 Call Stack에 쌓여있던 모든 것들이 모두 제거되면,

  차례대로 스택에 쌓여서 실행되게 함 (Event Loop) 

#### Web APIs

* 브라우저에서 제공하는 APIs
* 종류 : DOM, AJAX, Timeout 등...

#### Callback Queue(Task Queue)

* Web API 결과값을 쌓아두는 큐
* 처리할 메세지 목록과 실행할 콜백 함수들의 리스트

#### Event Loop

* 콜 스택과 콜백 큐를 관찰하는 역할
* Callback Event Queue에서 하나씩 꺼내 동작시키는 Loop
* **큐와 스택 두 부분을 지켜보고 있다가 스택이 비는 시점에 콜백을 실행시켜 주는 것**
* 이벤트 루프라는 것을 통해 자바스크립트에게 동시성을 지원하게 해줌 (진짜로 동시에 일어나는 것은 아님)

#### 3-1. 런타임 동작 예제

![자바스크립트 런타임 예제](https://beomy.github.io/assets/img/posts/javascript/javascript_runtime_settimeout.gif)

------

*자바스크립트는 싱글 스레드 프로그래밍 언어라 한번에 하나의 작업만 수행한다. 하지만 Web API, TaskQueue, EventLoop 덕분에 멀티 스레드처럼 실행하듯 보여진다.*



## :page_with_curl: Reference

[JavaScript 동작원리를 살펴봅시다](https://medium.com/humanscape-tech/javascript-%EB%8F%99%EC%9E%91%EC%9B%90%EB%A6%AC%EB%A5%BC-%EC%82%B4%ED%8E%B4%EB%B4%85%EC%8B%9C%EB%8B%A4-aef465c9c43)

[[JavaScript] 자바스크립트 런타임](https://beomy.github.io/tech/javascript/javascript-runtime/)

[javascript 동작 원리](https://velog.io/@namezin/javascript-%EB%8F%99%EC%9E%91-%EC%9B%90%EB%A6%AC)

[자바스크립트의 동작원리: 엔진, 런타임, 호출 스택](https://joshua1988.github.io/web-development/translation/javascript/how-js-works-inside-engine/)

[:writing_hand:공부하기|자바스크립트 동작 원리와 이벤트 루프(Event Loop)](https://kyung-a.tistory.com/11)

