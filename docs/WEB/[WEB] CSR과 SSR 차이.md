# [WEB] CSR과 SSR 차이

:writing_hand: *Assembled by JiYoung-Kwon (2021-01-06)* 



#### :pushpin: Rendering이란?

* 어떠한 웹 페이지 접속 시, 그 페이지를 화면에 그려주는 것

***



## 1. SPA(Single Page Application)

* 한 개의 페이지를 가진 어플리케이션
  * 사용자 친화적
  * 초기 렌더링 후 데이터만 받아옴 -> 상대적으로 서버 요청이 적음
  * Virtual Dom
  * Front-End와 Back-End 분리로 개발 업무 분업화 및 협업이 용이
  * 개발이 상대적으로 효율적
* **최초 한 번 페이지 전체를 로딩**. 이후 데이터만 변경하여 사용할 수 있는 웹 애플리케이션
* SPA는 기본적으로 CSR 방식을 사용한 것.  **SPA != CSR**

+) Angular, Vue, React : SPA 프레임워크



## 2. CSR(Client Side Rendering)

* 최초 요청 시 HTML을 비롯해 CSS, Javascript 등 각종 리소스를 받아온다.
* 이후에는 서버에 데이터만 요청하고, 자바스크립트로 뷰를 컨트롤 한다.

![img](https://media.vlpt.us/images/ru_bryunak/post/cd76c9fd-36c1-45dc-9015-ac99b27202f3/acca0a2e60d91ba7eef6a7967b6b7d2f.png)

#### 2-1. 장점

> * 첫 로딩에 HTML과 static파일들만 다 받으면, 동적으로 빠르게 Rendering -> 사용자 UX가 뛰어남
> * 서버에 요청하는 횟수가 훨씬 적어 서버 부담이 덜함

#### 2-2. 단점

> * 모든 HTML과 static 파일이 로드될 때까지 기다려야 함
> * SEO(검색엔진 최적화) 문제가 발생할 수 있음



+) 예시 페이지 소스 코드(Olive Platform - Kakao) //Angular

![kakao.png](./resources/kakao.png)

* 페이지 소스 코드에 콘텐츠 정보 없음

* 그렇다면 어떻게 화면이 그려졌을까? -> JavaScript로 그려짐

  > ![js.png](./resources/js.png)

* 콘텐츠가 달라져도 페이지 소스 코드는 동일함



## 3. SSR(Server Side Rendering)

* 서버에서 렌더링을 마치고, Data가 결합된 (완성된) HTML 파일을 내려주는 방식

  +) View로 return

* 요청 시 마다 새로고침이 일어나며 서버에 새로운 페이지에 대한 요청을 하는 방식

![img](https://media.vlpt.us/images/ru_bryunak/post/772ce7cf-f920-4373-8202-ed862e77c22e/546df7c4b04ea9ca5f72d822ca1d23b4.png)

#### 3-1. 장점

> * 초기 로딩 속도가 빨라 사용자가 콘텐츠를 빨리 볼 수 있음
> * 모든 검색엔진에 대한 SEO(검색엔진 최적화)가 가능함

#### 3-2. 단점

> * 매번 페이지를 요청할 때마다 새로고침 됨 -> 사용자 UX가 다소 떨어짐
> * 서버에 매번 요청을 하기에 트래픽, 서버 부하가 커짐



+) 예시 페이지 소스 코드 (Naver)

![naver.png](./resources/naver.png)

* 사용자 접근 시, div를 서버에서 만들어서 View에게 보내줌
* 콘텐츠에 대한 정보가 페이지 소스 코드에 포함되어 있음
* 콘텐츠가 달라지면 소스 코드도 바뀜



## 4. SEO(Search Engine Optimization) 문제

* 검색엔진 최적화 문제

  * 웹 페이지 검색엔진이 자료를 수집하고 순위를 매기는 방식에 맞게 웹 페이지를 구성해서 검색 결과의 상위에 나올 수 있도록 하는 작업

* `CSR`을 할 지 `SSR`을 할 지 고민하게 되는 이유

  * 공식 홈페이지와 같이 일반 사용자에게 검색되어야 하는 사이트라면 SEO 때문에 `SSR`에 대해 생각하게 됨

  > * CSR방식으로 이루어진 사이트 : View를 생성하기위해 자바스크립트를 실행시켜야 함
  >
  > * 대부분의 웹 크롤러 봇들은 자바스크립트 파일을 실행시키지 못함
  > * HTML 에서만 콘텐츠를 수집하게 되고 CSR 페이지를 빈 페이지로 인식하게 된다.
  >   * 구글은 크롤러 안에 자바스크립트 엔진이 들어있지만, 네이버나 다음 등의 검색엔진은 크롤링에 어려움이 있음



## 5. CSR vs SSR

![img](https://goodgid.github.io/assets/img/posts/ssr_and_csr_3.png)

|              | CSR                                                          | SSR                                                          |
| ------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 초기로딩속도 | 모든 JS 파일을 다운받아와야 함<br />**초기에 오래 걸린다**   | CSR에 비해 다운받는 파일이 많지 않음<br />**속도가 빠르다**  |
| 서버부담     | data 요청이 있을 때만 서버에 요청<br />**서버에 부담이 적음** | 서버와 잦은 응답(view 변경 시마다)<br />**서버에 부담이 됨** |
| SEO          | 맨 처음 HTML 파일이 비어있음<br />**크롤러가 데이터를 수집할 수 없음** (단, 구글 제외) | HTML에 대한 정보가 처음에 포함되어있음<br />**데이터 수집 가능** |



#### :pushpin: SSR과 CSR을 적절히 활용해야 한다!



## :page_with_curl: Reference

[CSR, SSR](https://velog.io/@namezin/CSR-SSR)

[SPA 그리고 SSR과 CSR](https://velog.io/@ru_bryunak/SPA-%EC%82%AC%EC%9A%A9%EC%97%90%EC%84%9C%EC%9D%98-SSR%EA%B3%BC-CSR)

[서버 사이드 렌더링(SSR)과 클라이언트 사이드 렌더링(CSR)](https://goodgid.github.io/Server-Side-Rendering-and-Client-Side-Rendering/)