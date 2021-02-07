# [WEB] 서블릿과 JSP

:writing_hand: *Assembled by JiYoung-Kwon (2021-01-31)* 



## 1. 서블릿 (Servlet)

```java
import java.io.*;
import javax.servlet.*;
import javax.servlet.http.*;

public ThreeParams extends HttpServlet {
    public void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        
        response.setContentType("text/html");
        printWriter out = response.getWriter();
        
        String title = "Reading Three Request Parameters";
        String docType = "<!DOCTYPE html PUBLIC \"-//W3C//DTD HTML 4.01 Transitional//EN\">\n";
        
        out.println(docType + 
            "<HTML>\n" +
            "<HEAD><TITLE>" + title + "</TITLE></HEAD>\n" +
            "<BODY BGCOLOR=\"#FDF5E6\">\n" +  
            "<H1 ALIGN=\"CENTER\">" + title + "</H1>\n" + 
            "<UL>\n" + 
            "<LI><B>param1</B>: " + request.getParameter("param1") + "\n" +
            "<LI><B>param2</B>: " + request.getParameter("param2") + "\n" +
            "<LI><B>param3</B>: " + request.getParameter("param3") + "\n" +
            "</UL>\n" +
            "</BODY></HTML>");
        )
    }
}
```

* **웹 기반의 요청에 대한 동적인 처리를 수행하기 위해 자바로 작성된 프로그램**
* .java가 확장자
* Java 코드 안에 HTML 코드
* 웹 개발을 위해 만든 표준
* Java 코드를 컴파일(.class 파일 생성)한 후 동적인 페이지를 처리함
  * Servlet이 수정된 경우, **전체 코드를 업데이트하고 다시 컴파일한 후 재배포하는 작업이 필요**
    * 개발 생산성 저하

------

*서블릿은 자바에 대한 지식이 필요하고 화면 인터페이스 구성에 너무 많은 코드들이 필요하는 등 비효율적 측면이 많다.*

*때문에 서블릿을 작성하지 않고 웹프로그래밍을 쉽게 할 수 있게 해주는 기술이 바로* ***JSP****이다.*

------

<br/>

## 2. JSP (Java Server Pages)

```html
<HTML>
<HEAD>
<TITLE>Reading Three Request Parameters</TITLE>
<LINK REL=STYLESHEET HREF="JSP-Styles.css" TYPE="text/css">
</HEAD>

<BODY>
<H1>Reading Three Request Parameters</H1>
<UL>
    <LI><B>param1</B>: <%= request.getParameter("param1") %>
    <LI><B>param2</B>: <%= request.getParameter("param2") %>
    <LI><B>param3</B>: <%= request.getParameter("param3") %>
</UL>
</BODY>
</HTML>
```

- **서블릿의 단점을 보완해서 만든 서블릿 기반의 서버 스크립트 기술**

  - Servlet의 모든 기능 + 추가적인 기능
- HTML 코드 안에 Java 코드
- JSP가 수정된 경우 **재배포할 필요 없이 WAS가 알아서 처리**함

  - 쉬운 배포

- ```
  스크립트 기술
  - ASP, PHP 처럼 미리 약속된 규정에 따라 간단한 키둬드를 조합하여 입력하면, 실행 시점에 각각의 키워드에 매핑이 되어 있는 어떤 코드로 변환 후에 실행되는 형태
  ```

<br/>

## 3. 서블릿 vs JSP

| Servlet                                                      | JSP                                                |
| ------------------------------------------------------------ | -------------------------------------------------- |
| **웹 기반 요청에 대한 동적 처리 가능한 서버 사이드 자바 프로그램** | **Java 언어 기반의 서버 사이드 스크립트 언어**     |
| 자바 코드안에 HTML 코드 존재(하나의 클래스)                  | HTML 코드 안에 자바 코드                           |
| HTML 태그를 문자열("") 스트림으로 처리                       | 자바코드를 <%%> 태그 안에 처리                     |
| 웹 개발을 위한 만든 표준                                     | 서블릿을 보완하고 기술을 확장한 스크립트 방식 표준 |
| DB와 통신, Bussiness Logic 호출, 데이터 리딩 체크 작업에 유용 | 요청 결과를 나타내는 HTML 작성시 유용              |
| Data Processing(Controller_ 다른 자바 클래스에 데이터를 넘겨주는 부분) 좋음 | Presentataion(View_보여지는 부분) 좋음             |
| 수정 시, 재배포 작업 필요                                    | 수정 시, 재배포 작업 필요 없음                     |

<br/>

## 4. 결론

- 결과적으로, **Servlet과 JSP는 만드는 방법에 차이가 있을 뿐 동일한 역할**을 함

- 초기에 자바 웹 개발은 서블릿을 이용한 개발이었으나, 이후 JSP 기술이 발표되면서 지금에서는 **Servlet과 JSP를 혼합하여 사용하는 형태**로 개발이 이루어지고 있다.

  > 대표적으로 **MVC 패턴** 이 있음
  >
  > [![servlet-jsp-model2](https://user-images.githubusercontent.com/58902042/105816666-ee081500-5ff7-11eb-9c9b-337f65f6eeb0.png)](https://user-images.githubusercontent.com/58902042/105816666-ee081500-5ff7-11eb-9c9b-337f65f6eeb0.png)
  >
  > * JSP와 Servlet을 모두 사용하여 프레젠테이션 로직과 비지니스 로직을 분리함
  > * **JSP**는 JSP기술의 장점을 최대한 활용 할 수 있는 웹에플리케이션 구조에서 사용자에게 결과를 보여주는 **프리젠테이션 층(View Lyaer)**을 담당
  > * **Servlet**은 Servlet기술의 장점을 최대한 활용 할 수 있는 사용자의 요청을 받아 분석하고 비지니스 층과 통신하여 처리하고 처리한 결과를 다시 사용자에게 응답하는 **컨트롤러 층(Controller Layer)**을 담당
  > * Model은 Java Beans로, DTO와 DAO를 통해 Mysql과 같은 Data Storage에 접근

<br/>

## :bulb: 예상질문

Q1 - 서블릿이란 무엇인가요?

A1 - 웹 기반의 요청에 대한 동적인 처리를 수행하기 위해 자바로 작성된 프로그램입니다.

<br/>

Q2 - JSP란 무엇인가요?

A2 - 서블릿을 사용하면서 생긴 비효율적인 측면들을 보완해서 만든 서블릿 기반의 서버 스크립트 기술입니다.

<br/>

Q3 - 서블릿과 JSP와 관련 있는 웹 개발 형태의 변화를 설명해보세요.

A3 - 초기에 자바 웹 개발은 서블릿을 이용한 개발이었으나, 이후 JSP 기술이 발표된 이후로 JSP는 presentation, 서블릿은 Data Processing에 강점을 좀 더 가지고 있어 최근에는 서블릿과 JSP를 혼합하여 사용하는 형태로 개발이 이루어지고 있습니다.

<br/>

## :page_with_curl: Reference

- [[Web\]Servlet과 JSP의 차이와 관계](https://gmlwjd9405.github.io/2018/11/04/servlet-vs-jsp.html)
- [JSP와 Servlet(서블릿) 비교](https://m.blog.naver.com/acornedu/221128616501)
- [기술면접 대비1- Servlet과 JSP의 차이](https://the-greatest-developer.tistory.com/2)
- [서블릿과 JSP란? 차이점은?](https://0ver-grow.tistory.com/161)