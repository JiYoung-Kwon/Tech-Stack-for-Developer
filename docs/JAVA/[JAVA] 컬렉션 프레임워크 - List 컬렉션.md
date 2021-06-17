# [JAVA] 컬렉션 프레임워크 - List 컬렉션

:writing_hand: *Assembled by JiYoung-Kwon (2021-03-07)* 



#### :pushpin: 컬렉션 프레임워크란?

* 프로그램 구현에 필요한 자료구조와 알고리즘을 구현해 놓은 라이브러리
* java.util 패키지에 포함. JDK 1.2부터 제공
* 개발에 소요되는 시간을 절약하고 최적화된 라이브러리를 사용할 수 있음
* 핵심 인터페이스
  * ![interface](https://blog.kakaocdn.net/dn/cl4iFr/btqw5hdraXw/Uty6Oxx28DvZ6Ea1WfmJAk/img.png)
* 자세한 내용 : [Java의 Collection - 참고](https://github.com/fake-developers/1st/blob/KJY-06/KJY/%5BJAVA%5D%20Collection.md)


***

<br/>

## 1. List 컬렉션

* 대표적인 List 컬렉션 클래스

  1. ArrayList<E\>
  2. LinkedList<E\>
  3. Vector<E\>
  4. Stack<E\>

* **인덱스 순서로** 저장이 되며, **중복된 데이터 저장 가능**

* 구조적으로 **데이터를 일렬로 늘여놓는 구조**

* 객체(데이터 등)를 저장하면, 인덱스가 자동으로 부여됨

  * 부여된 인덱스를 통해 데이터의 검색 및 삭제가 가능
  * 인덱스에는 데이터가 저장되어 있는 참조 값을 가짐 (객체 자체를 저장하는 것이 아님)

* 기본적인 List의 메소드

  * | 기능      | 메소드                                                       | 설명                                                         |
    | --------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
    | 객체 추가 | - boolean add(E element)<br /> - void add(int index, E element) <br />- E set( int index, E element) | - 해당 주어진 객체를 맨 끝 인덱스에 추가<br />- 해당 인덱스에 객체 추가<br />- 해당 인덱스에 주어진 객체로 변경 |
    | 객체 검색 | - boolean contains(Object object) <br />- E get(int index) <br />- boolean isEmpty() <br />- int size() | - 주어진 객체가 저장되어 있는지 여부 확인 <br />- 해당 인덱스에 저장된 객체 리턴 <br />- 켈렉션이 비어 있는지 조사 <br />- 저장되어 있는 전체 객체 수를 리턴 |
    | 객체 삭제 | - void clear() <br />- E remove(int index) <br />- boolean remove(Object o) | - 저장된 모든 객체를 삭제 <br />- 해당 인덱스 객체 삭제 <br />- 주어진 객체를 삭제 |
    | 기타      | - Iterator<E> iterator() <br />- boolean equals(Object o) <br />- Object[] toArray() | - 해당 리스트의 반복자(iterator)를 반환<br />- 해당 리스트와 전달된 객체가 같은지 확인 <br />- 해당 리스트의 모든 요소를 Object 타입의 배열로 반환 |

<br/>


## 2. ArrayList

* 저장 용량을 초과한 객체들이 들어오면 자동적으로 저장용량이 늘어나는 구조

  - 기본 생성자로 ArrayList 객체를 생성하면 내부에 10개의 객체를 저장할 수 있는 초기 용량을 가짐
  - 저장되는 객체 수가 늘어나면 자동적으로 증가하지만, 처음부터 크게 용량을 잡는 것이 가능
    - `ArrayList<String> list = new ArrayList<String>(30);`

* JDK 1.2 부터 제공된 ArrayList는 내부적으로 배열을 이용하여 객체 저장

  - 인덱스를 이용해 배열 요소에 빠르게 접근가능
  - 하지만 크기를 늘리기 위해서 새로운 배열을 생성하고 기존의 요소들을 옮겨야하는 복잡한 과정이 필요

* 특정 인덱스의 객체를 제거하면 바로 뒤 인덱스 부터 마지막 인덱스까지 모두 앞으로 1씩 당겨짐

  * 마찬가지로 특정 인덱스에 객체를 삽입하면 해당 인덱스부터 마지막 인덱스까지 모두 1씩 밀림

* 동기화를 보장하지 않음

  * 동기화가 필요할 때는 `Collections.synchronizeList()`메서드를 통해 동기화가 보장되는 List를 반환받아 사용

* 사용법

  * ```java
    ArrayList<E> arrList = new ArrayList<E>(); //기본 생성자 호출
    ```


#### 2-1. 예시

```java
ArrayList<Integer> arrList = new ArrayList<Integer>();

 
// add() 메소드를 이용한 요소의 저장
arrList.add(40);
arrList.add(20);
arrList.add(30);
arrList.add(10);


// for 문과 get() 메소드를 이용한 요소의 출력
for (int i = 0; i < arrList.size(); i++) {
    System.out.print(arrList.get(i) + " ");
} 
//실행결과 40 20 30 10

 
// remove() 메소드를 이용한 요소의 제거
arrList.remove(1);
 

// Enhanced for 문과 get() 메소드를 이용한 요소의 출력
for (int e : arrList) {
    System.out.print(e + " ");
}
//실행결과 40 30 10

 

// Collections.sort() 메소드를 이용한 요소의 정렬
Collections.sort(arrList);

 

// iterator() 메소드와 get() 메소드를 이용한 요소의 출력
Iterator<Integer> iter = arrList.iterator();

while (iter.hasNext()) {
    System.out.print(iter.next() + " ");
}
//실행결과 10 30 40 
 
// set() 메소드를 이용한 요소의 변경
arrList.set(0, 20);


for (int e : arrList) {
    System.out.print(e + " ");
}
//실행결과 20 30 40

// size() 메소드를 이용한 요소의 총 개수
System.out.println("리스트의 크기 : " + arrList.size());
//실행결과 리스트의 크기 : 3
```

- Collections 클래스
  - JDK 1.2부터 제공되는 컬렉션에서 동작하거나 컬렉션을 반환하는 클래스 메소드만으로 구성된 클래스
- Collections는 클래스, Collection은 인터페이스임을 주의해야 함

<br/>

## 3. LinkedList

* ArrayList가 배열을 이용하여 발생하는 단점을 극복하지 위해 고안

  - ArrayList와 비슷하지만, 선입 선출인 **Queue**와 양쪽 끝에서의 처리를 하는 **Deque**의 속성과 메소드를 가지고 있음

* 동기화를 보장하지 않음

  * 동기화가 필요할 때는 `Collections.synchronizeList()`메서드를 통해 동기화가 보장되는 List를 반환받아 사용

* JDK 1.2 부터 제공된 LinkedList는 *연결리스트*를 이용하여 요소 저장

  - **인접 참조를 링크해서 체인처럼 관리**
- 특정 인덱스의 객체를 제거하면 앞뒤 링크만 변경됨
  - 즉, 삽입/삭제가 빈번할 때 사용하는 것이 효율적
* 종류
  
  - **단일 연결 리스트(Singly LinkedList)**
    - 요소의 저장과 삭제 작업이 다음 요소를 가리키는 참조만 변경하면 되므로 아주 빠른 처리 가능
  - but, 현재 요소에서 이전 요소로 접근하기 매우 어려움
    - ![img](https://user-images.githubusercontent.com/58902042/109516034-18fbf200-7aeb-11eb-9ba9-1e25553c341f.png)
- **이중 연결리스트(Doubly LinkedList)**
    - 이전 요소를 가리키는 참조도 가짐
    - LinkedList 클래스도 위와 같은 이중 연결리스트를 내부적으로 구현한 것임
    - ![img](https://user-images.githubusercontent.com/58902042/109516397-77c16b80-7aeb-11eb-993d-539db8682e71.png)
  - **원형(환형) 연결리스트(Circular LinkedList)**
  * 일반적인 연결리스트에 마지막 노드와 처음 노드를 연결시켜 원형으로 만든 구조
  - **이중 원형(환형) 연결리스트(Doubly Circular LinkedList)**
    * 이중 연결리스트의 마지막 노드와 처음 노드를 연결시켜 원형으로 만든 구조
  
* 사용법

  * ```java
    LinkedList<E> lnkList = new LinkedList<E>();//기본 생성자 호출
    ```


#### 3-1. 예시

```java
LinkedList<String> lnkList = new LinkedList<String>();


// add() 메소드를 이용한 요소의 저장
lnkList.add("넷");
lnkList.add("둘");
lnkList.add("셋");
lnkList.add("하나");

 
// for 문과 get() 메소드를 이용한 요소의 출력
for (int i = 0; i < lnkList.size(); i++) {
   System.out.print(lnkList.get(i) + " ");
}
//실행결과 넷 둘 셋 하나

 
// remove() 메소드를 이용한 요소의 제거
lnkList.remove(1);
 

// Enhanced for 문과 get() 메소드를 이용한 요소의 출력
for (String e : lnkList) {
    System.out.print(e + " ");
}
//실행결과 넷 셋 하나


// set() 메소드를 이용한 요소의 변경
lnkList.set(2, "둘");
 
for (String e : lnkList) {
    System.out.print(e + " ");
}
//실행결과 넷 셋 둘


// size() 메소드를 이용한 요소의 총 개수
System.out.println("리스트의 크기 : " + lnkList.size());
//실행결과 리스트의 크기 : 3
```

- 위의 예제를 살펴보면 ArrayList와 LinkedList의 메서드가 거의 같은 것을 볼 수 있음

- 이처럼 **ArrayList와 LinkedList의 차이**는 사용 방법이 아닌, **내부적으로 요소를 저장하는 방법에 있음**

  - **ArrayList vs LinkedList**

    - | **구분**   | **순차적으로 추가/삭제** | **중간에 추가/삭제** | **검색** |
      | ---------- | ------------------------ | -------------------- | -------- |
      | ArrayList  | 빠르다                   | 느리다               | 빠르다   |
      | LinkedList | 느리다                   | 빠르다               | 느리다   |
  
  * **ArrayList와 LinkedList의 성능 비교**
  
    * | 비교항목                                                  |                  ArrayList                  |     LinkedList     |
      | :-------------------------------------------------------- | :-----------------------------------------: | :----------------: |
      | Element(Object)를 이용한 검색 [contains()]/삭제[remove()] |                    O(n)                     |        O(n)        |
      | index를 통한 Random 접근(get())                           |                    O(1)                     |        O(n)        |
      | index를 통한 삽입/삭제 - List의 중간                      |                    O(n)                     |        O(n)        |
      | Iterator를 통한 반복 중 1스탭                             |                    O(1)                     |        O(1)        |
      | Iterator를 통한 삽입/삭제 - List의 중간                   |                    O(n)                     |        O(1)        |
      | 개요                                                      | Dynamic (a.k.a. growable & resizable) array | Doubly-linked list |
      | 삽입/삭제 - 마지막 Element                                |           amortized O(1) [대부분]           |        O(1)        |
      | 삽입/삭제 - 최초 Element                                  |                    O(n)                     |        O(1)        |

<br/>

## 4. Vector

- JDK 1.0부터 사용해온 ArrayList 클래스와 같은 동작을 수행하는 클래스
  - ArrayList와 같은 구조를 가지고 있으나 동기화된 메서드로 구성되어 있어 멀티 쓰레딩 구조에 안정적임
- 과거에 대용량 처리를 위해 사용했으나, 비교적 성능이 좋지 않고 무거워 잘 쓰지 않음
  - 현재에는 기존 코드와의 호환성을 위해서만 남아있음

<br/>

## 5. Stack

- List 컬렉션 클래스의 Vector 클래스를 상속받아, 전형적인 스택 메모리 구조의 클래스를 제공

- LIFO(후입선출)의 자료구조

  - 가장 나중에 저장된 데이터가 가장 먼저 인출됨

  ![img](https://user-images.githubusercontent.com/58902042/109519767-e48a3500-7aee-11eb-997d-1035e91316a7.png)

- Stack 클래스는 스택 메모리 구조를 표현하기 위해, Vector 클래스의 메소드 5개를 상속받아 사용함

  | 메소드               | 설명                                                         |
  | -------------------- | ------------------------------------------------------------ |
  | boolean empty()      | 해당 스택이 비어 있으면 true를, 비어 있지 않으면 false를 반환 |
  | E peek()             | 해당 스택의 제일 상단에 있는(제일 마지막으로 저장된) 요소 반환 |
  | E pop()              | 해당 스택의 제일 상단에 있는(제일 마지막으로 저장된) 요소 반환 해당 요소를 스택에서 제거함. |
  | E push(E item)       | 해당 스택의 제일 상단에 전달된 요소를 삽입                   |
  | int search(Object o) | 해당 스택에서 전달된 객체가 존재하는 위치의 인덱스를 반환 이때 인덱스는 제일 상단에 있는(제일 마지막으로 저장된) 요소의 위치부터 0이 아닌 1부터 시작 |

- 더 복잡하고 빠른 스택을 구현하고 싶다면 Deque 인터페이스를 구현한 ArrayDeque 클래스를 사용함

  - 단, ArrayDeque 클래스는 Stack 클래스와 달리 search() 메서드를 지원하지 않음

* 사용법

  *  ```java
      Deque<E> st = new ArrayDeque<E>();
     ```

#### 5-1. 예시

  ```java
  Stack<Integer> st = new Stack<Integer>(); // 스택의 생성
  //Deque<Integer> st = new ArrayDeque<Integer>();
  
   
  
  // push() 메소드를 이용한 요소의 저장
  st.push(4);
  st.push(2);
  st.push(3);
  st.push(1);
  
   
  // peek() 메소드를 이용한 요소의 반환
  System.out.println(st.peek());
  //실행결과 1
  
  System.out.println(st);
  //실행결과 [4,2,3,1]
  
   
  
  // pop() 메소드를 이용한 요소의 반환 및 제거
  System.out.println(st.pop());
  //실행결과 1
  
  System.out.println(st);
  //실행결과 [4,2,3]
  
   
  
  // search() 메소드를 이용한 요소의 위치 검색
  System.out.println(st.search(4));
  //실행결과 3
  System.out.println(st.search(3));
  //실행결과 1
  ```

<br/>

## :page_with_curl: Reference

- [List 컬렉션 클래스](http://www.tcpschool.com/java/java_collectionFramework_list)
- [[Java/Collection] Java Collection Framework에 대한 이해를 통해 Data Structure 이해하기.](https://postitforhooney.tistory.com/entry/JavaCollection-Java-Collection-Framework에-대한-이해를-통해-Data-Structure-이해하기)
- [[Java]Collection Framework1 - List(ArrayList / Vector / LinkedList)](https://minhamina.tistory.com/14)
- [List 컬렉션](https://oper6210.tistory.com/35)
- [List 컬렉션2](https://hwan1001.tistory.com/5)
- [LinkedList](https://hwan1001.tistory.com/11)
