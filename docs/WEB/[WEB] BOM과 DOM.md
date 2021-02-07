# [WEB] BOM과 DOM

:writing_hand: *Assembled by JiYoung-Kwon (2021-01-10)* 



#### :pushpin: Window 객체

<img src="http://learn.javascript.ru/article/browser-environment/windowObjects@2x.png" width = "50%">

* 지금 보고 있는 브라우저 화면 창, 즉 **브라우저 전체를 담당하는 객체**
* 전역 객체
* Object Model - 웹 브라우저의 구성요소들은 객체화되어 있음
* Window 객체 아래에는 DOM, BOM, JavaScript가 있음
  * DOM : HTML/XML 문서 객체 모델, 주로 HTML 문서가 JavaScript 객체에 대응되는 것을 의미
  * BOM : 브라우저 객체 모델, 주로 JavaScript를 이용해 브라우저에 특정 기능을 수행시킬 때 사용 
  * JavaScript : 정적인 페이지를 동적으로 수정할 수 있게 도와주는 스크립트 언어

***



## 1. BOM(Browser Object Model)

* 브라우저와 컴퓨터 스크린에 접근할 수 있는 객체의 모음

* 자바스크립트가 **브라우저**와 소통하기 위해 만들어진 모델

  * 뒤로가기, 북마크, 즐겨찾기, 히스토리, URL 정보 등 브라우저가 가진 정보를 따로 객체화 시켜 관리

* Window 객체를 통해 접근 가능

  * window 객체 모델

    - `navigator` : 브라우저명과 버전 정보를 속성으로 가짐
    - `window` : 최상위 객체로, 각 프레임별 하나씩 존재
    - `document` : 현재 문서에 대한 정보
    - `location` : 현재 URL에 대 한 정보로 브라우저에서 사용자가 요청하는 URL
    - `history`: 현재의 브라우저가 접근했던 URL history
    - `screen` : 브라우저의 외부 환경에 대한 정보를 제공



## 2. DOM(Document Object Model)

* 문서에 대한 모든 내용을 담고 있는 객체
* HTML, XML 문서의 프로그래밍 인터페이스
  * HTML/XML **문서**를 브라우저에서 동적으로 제어하기 위해 탄생
  * 자바스크립트를 통해 동적으로 변경 가능
  * 문서와 문서의 요소(element)에 접근하기 위해 사용됨
* 객체지향 모델로써 구조화된 문서를 표현하는 형식



#### 2-1. 종류

* W3C DOM 표준은 3가지 모델로 구분됨 

  > 과거 각 브라우저 간 서로 상이한 DOM 구조로 인해 웹 페이지의 호환 문제가 컸음
  >
  > ->  W3C에서 DOM 표준 규격을 작성

  1. Core DOM : <u>모든</u> 문서 타입을 위한 DOM 모델
  2. HTML DOM : <u>HTML</u> 문서 타입을 위한 DOM 모델
  3. XML DOM : <u>XML</u> 문서 타입을 위한 DOM 모델



#### 2-2. DOM tree

* 웹 문서의 요소를 부모, 자식 요소로 구분할 수 있는 트리 구조로 구성

  ![img](https://media.vlpt.us/images/songsong2920/post/80e1c1c3-92bc-4b11-99e4-0fd729203620/253BB93956D506C722.png)

* **문서 노드 (Document Node)**

  > 트리의 최상위에 존재, 하위 자식 노드에 접근하기 위해서는 Document Node를 통해야 함
  >
  > Dom tree에 접근하기 위한 '시작점'

* **요소 노드 (Element Node)**

  > 웹 문서의 태그는 Element Node로 표현됨
  >
  > Attribute Node와 Text Node를 자식으로 가질 수 있음
  >
  > * 자식 노드를 변경하여 웹 페이지를 동적으로 조작할 수 있음

  * **속성 노드 (Attribute Node)**

    > 태그의 모든 속성은 Attribute Node로 표현

  * **텍스트 노드 (Text Node)**

    > 태그 내 텍스트를 표현
    >
    > Text Node는 자신의 자식 노드를 가질 수 없기 때문에 Dom tree의 '최종단'임



## :page_with_curl: Reference

[DOM과 Object Model](https://chaewonkong.github.io/posts/dom.html)

[[Javascript] BOM 과 DOM 이란?](https://heecheolman.tistory.com/35)

[BOM, DOM에 대한 설명.](https://velog.io/@songsong2920/DOM)

[[Javascript] Window,DOM,BOM이란?](https://cbw1030.tistory.com/46)