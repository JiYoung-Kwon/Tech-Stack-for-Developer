# [WEB] 브라우저 동작 과정

:writing_hand: *Assembled by JiYoung-Kwon (2021-01-17)* 



#### :pushpin: 웹 애플리케이션 구동 과정

1. **URL Entered**: 사용자가 웹 브라우저에서 사이트 주소를 입력
2. **DNS Lookup**: DNS를 이용하여 사이트 주소에 해당되는 Server IP 접근
3. **Socket Connection**: Client(브라우저)와 Server 간 접속을 위한 TCP 소켓 연결
4. **HTTP Request**: Client 에서 HTTP Header 와 데이터가 서버로 전송
5. **Content Download**: 해당 요청이 Server 에 도달하면 사용자가 원하는 문서를 다시 웹 브라우저에 전송
6. **Browser Rendering**: 웹 브라우저의 렌더링엔진에서 해당 문서를 다음과 같은 순서로 파싱

![./images/client-server.png](https://yilpe93.github.io/static/7efd177711cd81dd0712e9dd79eaf12c/fcda8/client-server.png)

## 1. 브라우저 주요 기능

* 사용자가 원하는 웹 페이지를 서버에 요청(Request)하고 서버의 응답(Response)을 받아 브라우저에 표시하는 것
* HTML, CSS 명세에 따라 HTML 파일을 해석해서 보여줌
  * 이 명세는 웹 표준화 기구인 W3C(World Wide Web Consortium)에서 정함

* 주요 요소
  * URI를 입력할 수 있는 주소 표시 줄
  * 이전 버튼과 다음 버튼
  * 북마크
  * 새로 고침 버튼과 현재 문서의 로드를 중단할 수 있는 정지 버튼
  * 홈 버튼
* 주요 브라우저
  * Google Chrome - Webkit
  * Safari - Webkit
  * Mozilla Firefox(Escape) - Gecko
  * Microsoft Internet Explorer
  * Opera

#### 1-1. 브라우저의 동작 과정

1. 브라우저가 서버로부터 HTML, CSS, JS, 이미지 파일등을 응답받음
2. HTML, CSS 파일이 렌더링 엔진의 HTML 파서와 CSS 파서에 의해 파싱됨
3. 파싱된 파일들이 DOM, CSSOM 트리로 변환되고 렌더 트리로 결합됨
4. 이렇게 생성된 렌더 트리를 기반으로 브라우저가 웹페이지를 표시

<br/>

## 2. 브라우저 기본 구조

1. 사용자 인터페이스
2. 브라우저 엔진 : 사용자 인터페이스와 렌더링 엔진 사이의 동작을 제어
3. **렌더링 엔진** : 요청한 콘텐츠를 표시(HTML, CSS 파싱/해석)
4. 통신 : HTTP 요청과 같은 네트워크 호출
5. UI 백엔드 : OS 사용자 인터페이스 체계를 사용
6. 자바스크립트 해석기 : JavaScript 코드 해석 및 실행
7. 자료저장소 : 쿠키같은 자원들을 저장하는 영역

![./images/browser_02.png](https://yilpe93.github.io/static/4ec9d46ea98033d0bf8d5c6966ba0462/0b533/browser_02.png)

<br/>

## 3. 렌더링 엔진

* 역할 : 요청 받은 내용을 브라우저 화면에 표시
| 브라우저 | 렌더링 엔진 |
| -------- | ----------- |
| IE       | Trident     |
| Chrome   | Webkit      |
| Safari   | Webkit      |
| Firefox  | Gecko       |
| Opera    | Presto      |

  #### 3-1. 렌더링 주요 동작 과정

![./images/browser_03.png](https://yilpe93.github.io/static/58dd63a5db0e6951536d1f080d54a9a0/fcda8/browser_03.png)

> 1. DOM Tree 생성
> 2. CSSOM(CSS Object Model) 생성
> 3. Render Tree(DOM + CSSOM) 생성
> 4. Render Tree 배치
> 5. Render Tree 그리기

* **HTML, CSS 각각의 파서**가 있음
  * **HTML은 각 태그들로 DOM 트리를 구성**
  * CSS도 스타일 규칙에 맞게 파싱 -> CSSOM 생성
  * 이후 같이 'Render Tree'를 생성
* 배치 시작 (각 노드가 화면의 정확한 위치에 표시되는 것을 의미)
* 그리기 과정 시작
* 모든 내용을 한 번에 파싱될 후 보여주기엔 속도가 느릴 수 있음
  * **기다리지 않고 파싱과 배치가 이뤄짐**
* 네트워크로부터 나머지 내용이 전송되기를 기다리는 동시에, 받은 내용의 **일부를 먼저 화면에 표시**

#### 3-2. 웹킷 동작 과정

![img](https://media.vlpt.us/images/zansol/post/44250de2-945a-4876-b038-c98278bd7ad8/image.png)

#### 3-3. 모질라의 게코 렌더링 엔진 동작 과정(3.6)

![img](https://media.vlpt.us/images/zansol/post/74f4ebaa-e8ab-4ffc-9806-e231b9326267/image.png)

<br/>

## 4. 파싱과 DOM 트리 구축

* 문서 파싱 : 브라우저가 코드를 이해하고 사용할 수 있는 구조로 변환하는 것

* 파싱 결과 : 보통 문서 구조를 나타내는 노드 트리

  * 파싱 트리(Parse Tree) 또는 문법 트리(Syntax Tree)라고 부름

* 두 가지로 구분

  * 어휘 분석(Tokenizing) : 문서의 자료를 토큰으로 분해하는 과정
  * 구문 분석 : 언어의 구문 규칙을 적용하는 과정

  ![./images/browser_05.png](https://yilpe93.github.io/static/a19d79568197571c6712eb948872fdf5/8e189/browser_05.png)

#### 4-1. HTML 파싱

* HTML 파서는 HTML 마크업을 파싱 트리로 변환

* XML에 반하여 HTML은 "유연한" 문법

* DOM : 문서 객체 모델(Document Object Model)

  * HTML의 내용과 속성을 Node로 갖고 각 Node의 관계를 나타내는 트리
  * HTML 문서를 구조화 하여 스크립트 또는 프로그래밍 언어에서 접근 가능한 형태로 제공
  * 문서 마크업의 속성과 관계를 포함하지만, 렌더링되어 그려질 때는 CSSOM이 관여함

* DOM은 마크업과 1:1 관계를 맺음

* 예시

  ```html
  <html>
  	<body>
  		<p>
  			Hello World
  		</p>
  		<div> <img src="example.png"/></div>
  	</body>
  </html>
  ```

  ![img](https://blog.kakaocdn.net/dn/b2yAzX/btqFeEkFT19/HAmNAhDXh35pTUghXc1svK/img.png)

#### 4-2. CSS 파싱

* HTML과 다르게 CSS는 문맥 자유 문법

* CSS 파일은 스타일 시트 객체로 파싱되고, 각 객체는 CSS 규칙을 포함

* CSSOM(CSS Object Model)

  * DOM 생성과 마찬가지로 태그들을 토큰화, 토큰을 Node로 변환하여 CSSOM으로 변환
  * 브라우저가 모든 CSS를 파싱하고 처리할 때까지 페이지가 화면에 그려지지 않음

* 예시

  ![img](https://blog.kakaocdn.net/dn/b2gImb/btqFe3ddBSz/x9Kethr4PD3MKuVQ0ZokXK/img.png)

#### 4-3. Render Tree

* DOM + CSSOM
* DOM의 Node에 일치하는 CSSOM 규칙을 찾아 연결
* 렌더링 트리에는 페이지를 렌더링하는 데 필요한 가시적인 Node만 포함됨
  * 메타 태그나 스크립트 태그 같은 Node 또는 `display : none` 스타일이 지정된 Node 는 제외됨
  * `visibility : hidden` 스타일이 적용된 Node는 보이지는 않지만 공간을 차지하므로 렌더링 트리에 포함됨
* Render Tree가 화면에 최종적으로 그려지는 내용이 됨  

## :page_with_curl: Reference

[브라우저 동작원리](https://velog.io/@zansol/%EB%B8%8C%EB%9D%BC%EC%9A%B0%EC%A0%80-%EB%8F%99%EC%9E%91%EC%9B%90%EB%A6%AC)

[브라우저 동작 원리](https://yilpe93.github.io/Web/browser/)

[브라우저 동작 원리 알아보기](https://jaddong.tistory.com/entry/%EB%B8%8C%EB%9D%BC%EC%9A%B0%EC%A0%80-%EB%8F%99%EC%9E%91-%EC%9B%90%EB%A6%AC-%EC%95%8C%EC%95%84%EB%B3%B4%EA%B8%B0)

[브라우저 동작 원리.](https://juunone.netlify.app/web/browser/)