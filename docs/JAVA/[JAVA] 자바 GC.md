# [JAVA] 자바 GC

:writing_hand: *Assembled by JiYoung-Kwon (2021-01-19)* 



## 1. GC란?

* Garbage Collection의 약자

  * Garbage : 정리되지 않은 메모리, 유효하지 않은 메모리 주소

  * 예시

    ```java
    String[] array = new String[2];
    
    array[0] = '0';
    array[1] = '1';
    
    array = new String[] {'G', 'C' };
    ```

    * String 배열이 할당되기 전에 할당된 0, 1
    * 주소를 잃어버려서 사용할 수 없는 메모리

  * 메모리가 부족할 때, 이런 가비지들을 메모리에서 해제시켜 다른 용도로 사용할 수 있게 해줌

* Java Runtime 시, Heap 영역에 저장되는 객체들은 따로 정리하지 않으면 계속해서 쌓이게 되어 OutOfMemory Exception이 발생할 수 있음

* 이를 방지하기 위해 JVM에서는 주기적으로 사용하지 않는 객체를 수집하여 정리하는 GC를 진행함

* 2가지 작업

  1. 힙(Heap) 내의 객체 중 Garbage를 찾아냄
  2. 찾아낸 Garbage 객체를 반환하여 메모리를 회수함

#### 1-1. 특징

<img src = https://t1.daumcdn.net/cfile/tistory/275F4333578E05A021 width = 60%>

* 객체들은 일단 생성되면 힙 영역에 생성됨
* 힙에 새로운 객체 생성 시, 공간이 부족하다면 JVM은 Out of MemoryGC를 뿌림
* GC는 Root Set of References(유효한 최초의 참조)가 이루어지지 않는 객체 Unrechable Objects들을 수거
* GC는 객체를 메모리에서 제거하기 전, 해당 객체의 finalize() 메소드를 호출
* GC는 사용자가 강제로 수행할 수 없고, 언제 일어나는지도 정확히 알 수 없음

#### 1-2. GC 전 후의 메모리

<img src = https://blog.kakaocdn.net/dn/pfb6e/btqy7LaVdLt/qeZ8DxJCPuKPLh4jZnFNP1/img.png width = 80%>

<img src=https://blog.kakaocdn.net/dn/dNtd6A/btqy8g9BsPc/xj3hC48Sj67glLHGiE1nc0/img.png width = 80%>

#### 1-3. GC 대상이 되는 객체

1. 모든 객체 참조가 null인 경우
2. 객체가 블럭 안에서 생성되고 블럭이 종료된 경우
3. 부모 객체가 null인 경우, 자식 객체는 자동적으로 GC 대상이 됨
4. 객체가 Weak 참조만 가지고 있을 경우
5. 객체가 Soft 참조이지만 메모리 부족이 발생한 경우

<br/>

## 2. JVM 메모리 영역

* GC 작업을 진행하는 Garbage Collector(가비지 콜렉터)는 GC를 위해 다음 역할을 함 

  1. 메모리 할당

  2. 사용중인 메모리를 인식

  3. 사용하지 않는 메모리를 인식

* 위 세가지 작업을 통해 앞으로 메모리를 얼마나 사용할 수 있는지 파악하고 GC를 언제 진행할지 지정할 수 있음

* JVM의 메모리 영역

  ![img](https://blog.kakaocdn.net/dn/bVFc8b/btqy8hALrbN/6KbAIdhlsa0lX7RetZvnN1/img.png)

  * Eden ~ Servior 까지를 Young 영역이라 함
  * 크게 Young, Old, Perm 영역으로 나눠지는데 JDK 8 버전부터는 이 영역이 사라짐
  * Young
    * 새로 생성한 객체가 위치
    * 대부분의 객체가 금방 unreachable(접근 불가능 상태)가 되기 때문에 많은 객체가 Young에 생성되었다가 사라짐
    * 이 영역에서 객체가 사라질 때, **Minor GC**가 발생한다고 함
  * Old
    * Young 영역에서 reachable 상태를 유지해 살아남은 객체가 복사됨
    * 대부분 Young 영역보다 크게 할당하며, 크기가 큰 만큼 Young 영역보다 GC는 적게 발생함
    * 이 영역에서 객체가 사라질 때, **Major GC**가 발생한다고 함
  * Perm
    * Method Area라고도 함
    * 클래스와 메소드 정보와 같이 자바 언어 레벨에서는 거의 사용되지 않는 영역
    * 이 영역에서 GC가 발생하면 Major GC의 횟수에 포함됨

<br/>

## 3. 객체 GC 과정

#### 3-1. stop-the-world

* GC를 실행하기 위해 JVM이 애플리케이션 실행을 멈추는 것
* 발생 시, GC를 실행하는 쓰레드를 제외한 나머지 쓰레드는 모두 작업을 멈춤
* GC 작업을 완료한 이후에야 중단했던 작업을 다시 시작함

#### 3-2. GC 과정

1. Marking

![img](https://t1.daumcdn.net/cfile/tistory/2424B949578E2E2741)

* 프로세스는 마킹을 호출함 -> 메모리가 사용되는지 아닌지를 찾아냄
* 참조되는 객체는 파란색, 참조되지 않는 객체는 주황색으로 보여짐
* 모든 오브젝트는 마킹 단계에서 결정을 위해 스캔됨 (매우 많은 시간 소모)

2 : Normal Deletion

![img](https://t1.daumcdn.net/cfile/tistory/243DEA3A578E2E3E0B)

* 참조되지 않는 객체를 제거하고, 메모리를 반환함
* 메모리 Allocator는 반환되어 비어진 블럭의 참조 위치를 저장해두고, 새로운 오브젝트가 선언되면 할당되도록 함

3 : Compacting

![img](https://t1.daumcdn.net/cfile/tistory/261C6D3A578E2E401C)

* 참조되지 않는 객체를 제거하고 남은 참조되는 객체들을 묶음
* 묶음으로써 공간이 생기므로, 새로운 메모리 할당 시 더 쉽고 빠르게 진행할 수 있음

-> 모든 객체를 mark & compact하는 JVM은 비효율적임



#### 3-2. Generational GC 과정

* 두 가정하에 만들어짐
  1. 대부분의 객체는 금방 접근 불가능 상태(unreachable)가 된다
  2. 오래된 객체에서 젊은 객체로의 참조는 아주 적게 존재한다



**1. 객체가 생성되어 Eden 영역에 올라감**

![img](https://blog.kakaocdn.net/dn/TrpMS/btqy7Jxvf7g/vhyeB91OAdQ4RZSGEU183K/img.png)

* 처음 생성된 객체는 Eden 영역에 할당됨
* 이후 Eden영역이 꽉 찬다면 할당이 해제되지 않은 객체를 Servior 영역으로 이동시킴 (minor gc 시작. 비 참조 객체는 Eden space가 clear 될 때 반환됨)

**2. Eden 영역이 꽉 차면 Servior영역으로 넘어감 (단 Servior 영역중 하나는 반드시 비어있어야 함)**

![img](https://blog.kakaocdn.net/dn/bEzeaG/btqy7JqM0em/8wnFa203IJzvG2poOk07ak/img.png)

* Servior 영역에 있는 객체는 올라가있는 Servior 영역이 꽉 찰 때 다시 GC 심사를 받음
* 할당이 되어있고 아직 사용중이라는 판단이 들면 다른 Servior 영역으로 이동
  * s1 이동 시, s0과 Eden 공간은 clear됨
  * minor GC 시, 이 과정 반복 (s1 -> s0 이동시, s1과 Eden 공간 clear)
* 여기서 Servior 영역을 거치지 않고 바로 Old 영역으로 이동하는 경우가 있음
  * 바로 객체의 크기가 Servior 영역의 크기보다 큰 경우

 **2-1. 객체의 크기가 Servior영역의 크기보다 큰 경우 Old 영역으로 이동**

![img](https://blog.kakaocdn.net/dn/bEPaoV/btqy9rQryU1/Ghs1XH8HlwnLQXFdsnZ6rk/img.png)

**3. 이 과정에서 오랫동안 살아남은 객체는 Old 영역으로 이동**

![img](https://blog.kakaocdn.net/dn/AQkly/btqy5SvDODb/LIASvjHwNeBPkgAJV1O3u1/img.png)

* Old 영역에 들어간 객체는 풀 GC, 메이저GC가 발생하지 않는한 GC되지 않음

#### 3-3. GC 종류

| 메이저 GC | Old, Perm 영역에서 발생하는 GC |
| :-------: | :----------------------------: |
| 마이너 GC |   Young 영역에서 발생하는 GC   |
|   풀 GC   | 메모리 전체를 대상으로 하는 GC |



## :page_with_curl: Reference

[가비지 컬렉터(GC)에 대하여](https://velog.io/@litien/%EA%B0%80%EB%B9%84%EC%A7%80-%EC%BB%AC%EB%A0%89%ED%84%B0GC)
[[JAVA] Garbage Collection의 기초](https://itmining.tistory.com/24)

[Java Garbage Collection](https://d2.naver.com/helloworld/1329)

[[Java] Java의 GC(Garbage Collection)방법과 종류](https://deveric.tistory.com/64)