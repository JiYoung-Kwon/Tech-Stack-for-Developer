# [JAVA] 자바 언어 동작 원리

:writing_hand: *Assembled by JiYoung-Kwon (2021-01-11)* 



## 1. 자바 프로그램 구동 원리

* 자바는 OS에 독립적인 특징을 가짐 (플랫폼 독립성. Platform Independent)

  -> JVM(Java Virtual Machine) 위에서 동작하도록 만들어졌기 때문

![img](https://t1.daumcdn.net/cfile/tistory/997B2B3A5B757CBF14)

* 일반 프로그램 : "운영체제"가 프로그램을 실행
* 자바 프로그램 : 운영체제가 JVM을 실행시키면 "JVM"이 프로그램(클래스 파일을 실행)

![img](https://t1.daumcdn.net/cfile/tistory/99B3F53B5B7579C909)

1. 소스코드를 작성 (.java 확장자의 소스 파일)

2. 컴파일러(javac.exe)가 바이트 코드로 변환 (.class 확장자의 클래스 파일)

   > 바이트 코드(byte code)
   >
   > * JVM이 이해할 수 있는 언어로 변환된 코드
   > * 아직 컴퓨터는 읽을 수 없는 **반기계어**
   > * JVM만 설치되어 있다면 바이트 코드는 **어떤 운영체제에서라도 실행**될 수 있음

3. 런처(java.exe)로 자바 가상 머신(JVM)을 구동시킴

4. 자바 가상 머신이 바이트 코드를 해석하여 자바 프로그램이 실행됨



## 2. JVM 내 동작 과정

![img](https://blog.kakaocdn.net/dn/b8Ggxw/btqDbFdEZdY/Ho1kpzsNqFz3Pbpy8OfiFk/img.png)

1. 컴파일된 바이트 코드를 JVM의 **클래스 로더**에게 전달

   > 클래스 로더 세부 동작
   >
   > 1. 로드 : 클래스 파일을 가져와 JVM의 메모리에  로드
   > 2. 검증 : 자바 언어 명세(Java Language Specification) 및 JVM 명세에 명시된 대로 구성되어 있는지 검사
   > 3. 준비 : 클래스가 필요로 하는 메모리를 할당 (필드, 메서드, 인터페이스 등)
   > 4. 분석 : 클래스의 상수 풀 내 모든 심볼릭 레퍼런스를 다이렉트 레퍼런스로 변경
   > 5. 초기화 : 클래스 변수들을 적절한 값으로 초기화 (static 필드)

2. 클래스 로더는 **동적 로딩(Dynamic Loading)**을 통해 필요한 클래스들을 로딩 및 링크하여 **런타임 데이터 영역(Runtime Data area), 즉 JVM의 메모리**에 올림

3. **실행엔진(Execution Engine)**은 JVM 메모리에 올라온 바이트 코드를 명령어 단위로 하나씩 가져와서 실행 (**2가지 방식**으로 동작)

   > 1. 자바 인터프리터
   >    * 바이트 코드 명령어를 하나씩 읽어 해석하고 실행
   >    * 하나하나의 실행은 빠르나, 전체적인 실행 속도가 느림
   > 2. JIT 컴파일러 (Just-In-Time Compiler)
   >    * 인터프리터의 단점을 보완하기 위해 도입된 방식
   >    * 바이트 코드 전체를 컴파일하여 바이너리 코드로 변경, 이후에는 해당 메서드를 더이상 인터프리팅하지 않고 바이러니 코드로 직접 실행
   >    * 전체적인 실행 속도는 인터프리팅 방식보다 빠름



## :page_with_curl: Reference

[Java의 동작원리와 JVM의 역할](https://swk3169.tistory.com/181)

[자바의 구동 원리와 JVM(Java Virtual Machine)](https://gbsb.tistory.com/2)

[[JAVA] JAVA 동작원리 및 JVM](https://devs-k.tistory.com/10)

