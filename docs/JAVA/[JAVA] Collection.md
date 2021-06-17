# [JAVA] Collection

:writing_hand: *Assembled by JiYoung-Kwon (2021-03-07)* 

<br/>



## 1. Java Collection Framework

* **Collection 객체**
* 데이터의 집합, 그룹 (컨테이너)
* 여러 원소들을 담을 수 있는 자료구조
* 배열과 비슷하지만 크기가 고정된 배열의 문제점을 보완함

<br/>

#### 1-1. Java Collection Framework (JCF)

* 이러한 데이터, 자료구조인 컬렉션과 이를 구성하는 클래스를 정의하는 인터페이스를 제공함
* 즉, 컬렉션을 다루기 위한 표준화 프로그래밍 방식

* 배열의 문제점을 해결하고, 널리 알려져 있는 자료구조를 바탕으로 객체들을 효율적으로 추가, 삭제, 검색할 수 있도록 함
* **java.util 패키지에 컬렉션과 관련된 인터페이스와 클래스들을 포함시킨 것**
  * 컬렉션 인터페이스 : java.util 패키지
  * 컬렉션 클래스 : java.util 또는 java.util.concurrent 패키지

* 자바 초기에는 Vector, Stack, HashTable 등의 컬렉션 클래스만 제공하였음

  * 자바 1.2이후로 컬렉션을 다루기 위해 컬렉션 프레임워크가 등장

* **장점**

  - 코딩 시간 감소

  - 코드 품질 보장

  - 유지보수 시간 감소

  - 재사용 가능 & 상호 운용성 보장

    ```
    상호 운용성
    
    하나의 시스템이 동일 또는 이기종의 다른 시스템과 아무런 제약이 없이 서로 호환되어 사용할 수 있는 성질
    ```


<br/>

#### 1-2. 컬렉션 프레임워크 계층구조

- Collection 인터페이스는 크게 List, Set, Queue로 3개의 상위 인터페이스로 분류
- **Map의 경우** Collection 인터페이스를 상속받고 있지 않지만 Collection으로 분류함
  - Map은 **구조상의 차이(Key-Value)로** 인해 별도로 정의

[![img](https://user-images.githubusercontent.com/58902042/109483408-89dae400-7ac2-11eb-8fde-510d29be2969.png)](https://user-images.githubusercontent.com/58902042/109483408-89dae400-7ac2-11eb-8fde-510d29be2969.png)

<br/>

- **Collection Interface** : 데이터를 순서, 집합 형태의 저장공간에 담음
  1. Set : 순서를 유지하지 않은 상태로 데이터를 저장, 동일한 데이터를 중복 저장할 수 없음
  2. List : 순서를 유지한 상태로 데이터를 저장, 중복 저장 가능
  3. Queue : List와 흡사, 처리 전 요소를 보유하는데 사용

[![img](https://user-images.githubusercontent.com/58902042/109483475-a0813b00-7ac2-11eb-9251-3c81371d0eae.png)](https://user-images.githubusercontent.com/58902042/109483475-a0813b00-7ac2-11eb-9251-3c81371d0eae.png)

<br/>

- **Map Interface** : Key - Value 형태의 저장공간에 데이터를 담음
  1. Map : Key와 Value를 하나의 쌍으로 묶어서 관리, Key는 중복 저장 불가

[![img](https://user-images.githubusercontent.com/58902042/109483510-ad9e2a00-7ac2-11eb-9e7f-81e62f6982d9.png)](https://user-images.githubusercontent.com/58902042/109483510-ad9e2a00-7ac2-11eb-9e7f-81e62f6982d9.png)

<br/>

## 2. 컬렉션 인터페이스(Collection Interface)

* 제네릭(Generics)으로 표현
  * 컴파일 시점에서 객체의 타입을 체크하기 때문에 런타임 에러를 줄이는 데 도움이 됨
    * ex) 런타임 시 발생하는 ClassCastException을 컴파일 시점에서 찾아낼 수 있음
      * 클래스 캐스팅을 하지 않아도 됨
      * instanceof를 사용하지 않아도 되므로 코드를 좀 더 깔끔하게 유지할 수 있음
  * 클래스를 자료형에 상관없이 사용할 수 있음

* 컬렉션 인터페이스의 분류
  * **Collection 인터페이스**
  * **Map 인터페이스**
    * 구조상의 차이(Key-Value)로 인해 Collection 인터페이스를 상속받지 않고 별도로 정의됨
  * **기타 인터페이스**

<br/>

#### 2-1. Collection 인터페이스 그룹

* 직접적인 구현은 제공하지 않으며, 모든 컬렉션 클래스가 구현해야 하는 메서드를 포함하고 있음

<br/>

1. **List 인터페이스**

   * 순서가 있는 컬렉션
   * 중복 요소를 포함할 수 있음
   * 인덱스로 모든 요소에 접근할 수 있음
   * List 인터페이스로 구현된 클래스 : ArrayList, Linkedlist

2. **Set 인터페이스**

   * 중복요소를 포함할 수 없음
   * 랜덤 액세스(Random access)를 허용하지 않음
   * iterator 또는 foreach를 이용하여 요소를 탐색할 수 있음
   * Set 인터페이스로 구현된 클래스 : HashSet, TreeSet, LinkedHashSet

3. **SortedSet 인터페이스**

   - 요소를 오름차순으로 유지하는 Set

4. **Queue 인터페이스**

   - 처리전의 요소를 보유하는데 사용

   - FIFO 정렬, 예외적으로 우선순위 큐가 존재

5. **Deque 인터페이스**

   - 양쪽 끝에 요소 삽입 및 제거를 지원함

<br/>

* **대표적인 메소드들**
  * boolean add(E e) : 해당 컬렉션에 전달된 요소를 추가
  * boolean remove(Object o) : 해당 컬렉션에서 전달된 객체를 제거
  * void clear() : 해당 컬렉션의 모든 요소를 제거
  * boolean contains(Object o) : 해당 컬렉션이 전달된 객체를 포함하고 있는지
  * boolean equals(Object o) : 해당 컬렉션과 전달된 객체가 같은지
  * boolean isEmpty() : 해당 컬렉션의 반복자(iterator)를 반환
  * int size() : 해당 컬렉션의 요소의 총개수를 반환
  * Object [] toArray() : 해당 컬렉션의 모든 요소를 Object 타입의 배열로 반환

<br/>

#### 2-2. Map 인터페이스 그룹

1. **Map 인터페이스**

   * 키와 값을 매핑

   * 중복 키가 존재할 수 없으며 각 키는 하나의 값만 매핑할 수 있음

   * Map의 기본 연산

     * put, get, containsKey, containsValue, size, isEmpty등
   
   * Map 인터페이스로 구현된 클래스 : HashMap, TreeMap, LinkedHashMap
   
2. **SortedMap 인터페이스**

   * 매핑을 오름차순의 키 순서로 유지하는 Map

<br/>

#### 2-3. 기타 인터페이스 그룹

1. **Iterator 인터페이스**

   * 어떤 컬렉션이든 반복적으로 수행하기 위한 메서드를 제공
   * 컬렉션 프레임워크에서는 Enumeration 대신 Iterator를 사용
   * 컬렉션 클래스의 Iterator는 Iterator 디자인 패턴을 구현함
   * iterator 메서드를 통해 컬렉션으로부터 iterator instance를 가져올 수 있고, 컬렉션을 순회하는 도중에 엘리먼트들을 삭제할 수 있음

   ```
   Enumeration 인터페이스
   
   객체들의 집합(Vector)에서 각각의 객체들을 한순간에 하나씩 처리할 수 있는 메소드를 제공하는 컬렉션이다.
   ```

2. **ListIterator 인터페이스**

   * Iterator를 상속한 인터페이스, List에서 제공하는 인터페이스

     * List 인터페이스에서만 listIterator() 메서드 사용 가능

   * 어느 방향이든(양방향) 목록을 탐색하고 반복하면서 목록을 수정하고, 목록에서 반복자의 현재 위치를 가져올 수 있음

   * ListIterator에는 현재의 요소가 없음

     * 커서 위치는 항상 previous()에 대한 호출에 의해 반환될 요소와 next()에 대한 호출에 의해 반환될 요소 사이에 위치함

   * ```java
     LinkedList<Integer> lnkList = new LinkedList<Integer>();
     
     lnkList.add(4);
     lnkList.add(2);
     lnkList.add(3);
     lnkList.add(1);
     
     
     ListIterator<Integer> iter = lnkList.listIterator();
     
     while (iter.hasNext()) {
         System.out.print(iter.next() + " ");
     }
     //실행결과 4 2 3 1
      
     
     while (iter.hasPrevious()) {
         System.out.print(iter.previous() + " ");
     }
     //실행결과 1 3 2 4
     ```

3. **Concurrent 인터페이스 그룹**

   - BlockingQueue 인터페이스
   - TransferQueue 인터페이스
   - BlockingDeque 인터페이스
   - ConcurrentMap 인터페이스
   - ConcurrentNavigableMap 인터페이스

<br/>

## 3. 컬렉션 클래스(Collection Class)

* 컬렉션 프레임워크는 컬렉션 인터페이스에 대한 **구현 클래스** 를 제공함

- 컬렉션 클래스의 종류
  - **일반적으로 쓰이는 클래스**
    - ArrayList, LinkedList, HasSet, TreeStet, PriorityQueue, ArrayDeque, HashMap, TreeMap, LinkedHashMap
  - **Concurrent 클래스**
    - CopyOnWriteArrayList, ConcurrentHashMap, CopyOnWriteArraySet
  - **Legacy 클래스** 
    - Vector, Stack, Dictionary, Hashtable, Properties
  - **Abstract 클래스** 
    - AbstractList, AbstractSequenctailList, AbstractSet, AbstractQueue

#### 특징

| 컬렉션 클래스        | 순서 | 랜덤 액세스 | 키 - 값 | 중복 요소 | 널 요소 | 스레드 안전 |
| -------------------- | ---- | ----------- | ------- | --------- | ------- | ----------- |
| ArrayList            | O    | O           |         | O         | O       |             |
| LinkedList           | O    |             |         | O         | O       |             |
| HashSet              |      |             |         |           | O       |             |
| TreeSet              | O    |             |         |           |         |             |
| Hashmap              |      | O           | O       |           | O       |             |
| Treemap              | O    | O           | O       |           |         |             |
| CopyOnWriteArrayList | O    | O           |         | O         | O       | O           |
| CopyOnWriteArraySet  |      |             |         |           | O       | O           |
| ConcurrentHashMap    |      | O           | O       |           |         | O           |

<br/>

## 4. 컬렉션즈 클래스(Collections Class)

- **collection 인터페이스를 구현한 클래스에 대한** 객체생성, 정렬(sort), 병합(merge), 검색(search)등의 기능을 안정적으로 수행하도록 도와주는 역할
- 컬렉션에서 작동하거나 반환하는 정적 메서드로만 구성됨
  - static 메서드이기 때문에 인스턴스를 생성하지 않고 바로 사용 가능
- **Collections와 Collection은 다르다!**
- 자주 사용되는 알고리즘으로는 `정렬(sorting)`, `섞기(shuffling)`, `탐색(searching)`등이 있음
- 주요 메서드
  - max() : 지정된 컬렉션에서 최대 요소 반환 (인덱스 X)
  - min() : 지정된 컬렉션에서 최소 요소 반환(인덱스 X)
  - **sort()** : 지정된 컬렉션을 정렬. 오버로드 메소드들이 존재하며 가장 기본적인 메소드는 자연순서에 따라 내림차순으로 정렬
  - **shuffle()** : 지정된 컬렉션의 요소들의 순서를 무작위로 섞음
  - synchronizedCollection() : 지정된 컬렉션에 의해 지원되는 동기화 된 컬렉션을 재생성해 반환
  - **binarySearch()** : 지정된 컬렉션에서 이진 탐색 알고리즘을 사용해 지정된 객체를 검색해 인덱스 반환
  - disjoint() : 2개의 지정된 컬렉션들에서 공통된 요소가 하나도 없는 경우 true 를 반환
  - copy() : 지정된 켈렉션의 모든 요소를 새로운 컬렉션으로 복사 후 반환
  - reverse() : 지정된 컬렉션에 있는 순서를 역으로 변경

<br/>

**:pushpin: 주의할 점! 자바의 Collection은 인터페이스며, Collections는 클래스이다**

<br/>

## 5. 컬렉션 프레임워크의 모범 사례

- 크기(size)가 고정되어 있다면 ArrayList보다 **Array**를 사용하라.
- 맵에 삽입된 순서대로 iterate를 하고 싶으면 **TreeMap**을 사용하는 것이 좋다.
- 중복을 허용하고 싶지 않으면 **Set**을 사용하면 된다.
- 몇몇 컬렉션 클래스들을 초기 용량을 지정할 수 있다. 만약 저장할 요소들의 사이즈를 알 경우에 **초기 용량**을 지정함으로써 rehashing이나 resizing이 일어나는 것을 회피할 수 있다.
- 코드를 작성할 때, 구현 클래스가 아닌 **인터페이스**를 기반으로 작성해야 나중에 구현체를 변경할 때 코드를 재작성하는 수고를 줄일 수 있다.
- 런타임에 발생할 수 있는 ClassCastException을 회피하려면 항상 **제네릭(Generics)을** 사용해서 type-safety 한 상태를 유지하라.
- 맵에 키를 사용할 때 JDK에서 제공하는 **immutable** 클래스를 사용하여 사용자 클래스에서 hashCode()와 equals() 구현할 필요가 없게 하라
- 읽기 전용 및 동기화, 빈 컬렉션 등을 만들 때는 자신만의 구현으로 생성하지 말고 Collections에서 제공하는 **유틸리티 클래스**를 사용하라. 이는 코드 재사용성을 높여주고 안정적이며 유지보수 비용을 줄여 준다.

<br/>

## :page_with_curl: Reference

- [Java 컬렉션 정리1](https://gangnam-americano.tistory.com/41)
- [Java 컬렉션 정리2](https://www.crocus.co.kr/1553)
- [Java 컬렉션 정리3](https://gbsb.tistory.com/247#java-collections-algorithms)
- [Java 컬렉션 정리4](https://shlee0882.tistory.com/97)
- [상호운용성](https://ko.wikipedia.org/wiki/상호운용성)
- [Enumeration](https://hyeonstorage.tistory.com/210)

- [[Java] Collection Framework1 - List(ArrayList / Vector / LinkedList)](https://minhamina.tistory.com/14)
- [자바 컬렉션 프레임워크(Java Collection Framework) 정리](https://gbsb.tistory.com/247)
- [[JAVA] Java 컬렉션(Collection) 정리](https://gangnam-americano.tistory.com/41)
- [[Java] 컬렉션 프레임워크 - List, Set, Queue, ArrayList, LinkedList, Iterator, Stack, Tree, Map](https://butter-shower.tistory.com/89)
- [자바공부-5.List 인터페이스와 ListIterator 인터페이스](https://scarlett.tistory.com/entry/자바공부-5List-인터페이스와-ListIterator-인터페이스)
- [Collections 클래스](https://velog.io/@gillog/Collections-클래스)