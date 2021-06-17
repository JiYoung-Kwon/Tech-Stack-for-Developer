# [JAVA] 컬렉션 프레임워크 - Set 컬렉션

:writing_hand: *Assembled by JiYoung-Kwon (2021-03-02)* 



#### :pushpin: 컬렉션 프레임워크란?

* 프로그램 구현에 필요한 자료구조와 알고리즘을 구현해 놓은 라이브러리
* java.util 패키지에 포함. JDK 1.2부터 제공
* 개발에 소요되는 시간을 절약하고 최적화된 라이브러리를 사용할 수 있음
* 핵심 인터페이스
  * ![interface](https://blog.kakaocdn.net/dn/cl4iFr/btqw5hdraXw/Uty6Oxx28DvZ6Ea1WfmJAk/img.png)
* 자세한 내용 : [Java의 Collection - 참고](https://github.com/fake-developers/1st/blob/KJY-06/KJY/%5BJAVA%5D%20Collection.md)


***

<br/>

## 1. Set 컬렉션

* HashSet, LinkedHashSet, TreeSet 등이 있음

* 순서가 존재하지 않는 비선형적인 자료구조

  * List 컬렉션과 다르게 **저장 순서가 유지되지 않음**

* **중복을 허용하지 않는** 구조

  * 객체를 중복해서 저장할 수 없음 
  * 중복 데이터 제거 수단으로 사용됨

* 하나의 null만 저장할 수 있음

* Set 인터페이스는 단독으로 객체를 만들 수 없음

    * 하위 클래스인 HashSet, TreeSet 등을 통해 다운캐스팅하여 만들어야 함

* **인덱스가 없음**

  * 위치 기반으로 데이터를 가져올 수 없음

  * 인덱스를 파라미터로 갖는 메소드가 존재하지 않음

  * 대신, 전체 객체를 대상으로 한 번씩 반복해서 가져오는 **반복자(Iterator)를 제공**

    * 반복자 : Iterator 인터페이스를 구현한 객체, iterator() 메소드 호출 시 얻을 수 있음

    * 사용법

      * ```java
        Set<String> set = new HashSet<String>();
        Iterator<String> iterator = set.iterator();
        ```

    * 반복자를 얻고 아래 메소드를 이용할 수 있음

      * | 리턴 타입 | 메소드 명 | 설명                                           |
        | --------- | --------- | ---------------------------------------------- |
        | Boolean   | hasNext() | 가져올 객체가 있으면 true를 리턴, 없으면 false |
        | E         | next()    | 컬렉션에서 하나의 객체를 가져옴                |
        | void      | remove()  | Set 컬렉션에서 객체를 제거함                   |

      * ```java
        Set<String> set = new HashSet<String>();
        	
        set.add("안녕하세요.");
        set.add("반갑습니다.");
        		
        Iterator<String> iterator = set.iterator();
        
        while(iterator.hasNext()){
        	//String 객체 하나를 가져옴
        	String str = iterator.next();
        	System.out.println(str);
        }
        ```

#### 1-1. Set 인터페이스 메소드

* Set 컬렉션에서 공통적으로 사용 가능한 Set 인터페이스의 메소드들

    * | add()         | addAll()  | clear()     | contains()  |
      | ------------- | --------- | ----------- | ----------- |
      | containsAll() | equals()  | hashCode()  | isEmpty()   |
      | iterator()    | remove()  | removeAll() | retainAll() |
      | size()        | toArray() |             |             |
      
    * boolean add (E e)처럼 E라는 타입 사용

      * Set 인터페이스가 제네릭 타입이기 때문
      * 구체적인 타입은 구현 객체를 생성할 때 결정됨

    * 사용법

      * ```java
        Set<String> set = new Set<String>();
        set.add("Andy");
        set.add("Kush"); //객체 추가
        set.remove("Andy"); //객체 삭제
        ```

<br/>


## 2. HashSet

* Set 인터페이스의 구현 클래스

* 사용법

  * ```java
    Set<E> set = new HashSet<E>(); //기본 생성자 호출
    ```

  * 타입 파라미터 E에는 컬렉션에 저장할 객체 타입을 지정

* 객체들을 순서 없이 저장하고 동일한 객체는 중복 저장하지 않음

  * 저장 순서를 유지하고자 한다면 `LinkedHashSet`을 사용해야 함
  * 기본적으로 정렬이 불가능함
    * `NavigableSet<E>`을 구현한 `TreeSet<E>`은 정렬 기능을 가짐 - [아래](#TreeSet)

* 과정

  1. 객체를 저장하기 전에 먼저 객체의 **hashCode**() 메소드를 호출해서 **해시코드를** 얻어냄
  2. 이미 저장된 객체들의 해시코드와 비교
  3. 동일한 해시코드가 있다면, 다시 equals() 메소드로 두 객체를 비교
     * true가 나오면 동일한 객체로 판단하고 중복 저장을 하지 않음

#### 2-1. 메소드 오버라이딩

* **문자열을 HashSet에 저장할 경우**

  * 같은 문자열을 갖는 String 객체는 동등한 객체로 간주됨
  * 다른 문자열을 갖는 String 객체는 다른 객체로 간주됨
  * 이유
    * String 클래스가 hashCode()와 equals() 메소드를 오버라이딩하여 같은 문자열일 경우 hashCode()의 리턴 값을 같게, equals()의 리턴값은 true가 나오도록 했기 때문

* **hashCode()와 equals() 메소드 오버라이딩**

  * 예시 - 인스턴스가 달라도 이름과 나이가 동일하다면 동일한 객체로 간주하여 중복 저장되지 않도록 하는 경우

  * Member.java

    * ```java
      package set;
       
      public class Member {
          public String name;
          public int age;
       
          public Member(String name, int age) {
              super();
              this.name = name;
              this.age = age;
          }
       
          @Override
          public boolean equals(Object obj) {
              if (obj instanceof Member) {
                  Member member = (Member) obj;
                  return member.name.equals(name) && (member.age == age);
              } 
              else {
                  return false;
              }
          }
       
          @Override
          public int hashCode() {
              return name.hashCode() + age;
          }
       
      }
      ```

  * HashSetExam2.java

    * ```java
      package set;
       
      import java.util.HashSet;
      import java.util.Iterator;
      import java.util.Set;
       
      public class HashSetExam2 {
       
          public static void main(String[] args) {
              Set<Member> set = new HashSet<Member>();
              
              set.add(new Member("Jackie", 22));
              set.add(new Member("Jackie", 22));
              set.add(new Member("Hong", 24));
              set.add(new Member("Andy", 32));
              set.add(new Member("Jolie", 29));
              
              System.out.println("총 객체 수: " + set.size());
              
              Iterator<Member> it = set.iterator();
              
              while (it.hasNext()) {
                  Member mem = it.next();
                  System.out.println("\t" + mem.name + " - " + mem.age);
              }
          }
       
      }
      ```

* +) **해쉬 알고리즘과 hashCode 메소드**

  - 동일한 인스턴스의 존재 여부를 확인하는 클래스가 HashSet<E\>

  - 즉 탐색 과정은
    - 1단계 : Object 클래스에 정의된 hashCode 메소드의 반환 값을 기반으로 부류 결정
    - 2단계 : 선택된 부류 내에서 eqauls 메소드를 호출하여 동등 비교

  - Object 클래스에 정의되어 있는 hashCode와 equals 메소드는 다음과 같이 정의되어 있음
    - 인스턴스가 다르면 Object 클래스의 hashCode 메소드는 다른 값을 반환
    - 인스턴스가 다르면 Object 클래스의 equals 메소드는 false를 반환
  - 참고로, Object 클래스의 hashCode 메소드는 인스턴스가 저장된 **주솟값**을 기반으로 반환 값이 만들어지도록 정의되어 있음
    - 즉, Object 클래스의 hashCode와 equals는 저장하고 있는 값을 기준으로 동등 여부를 따지지 않음
    - 값을 기준으로 동등 여부를 따지려면 두 메소드를 오버라이딩 해야 함

<br/>

## 3. TreeSet

* 이진 트리 구조를 기반으로 한 `Set<E>` 계열의 컬렉션

* **이진 검색 트리(binary search tree) 자료구조**의 형태로 데이터를 저장

  * 이진 검색 트리

    * 정렬, 검색, 범위검색(range search)에 높은 성능을 보이는 자료구조

    * ![img](https://blog.kakaocdn.net/dn/bsMoMr/btqANDbFFhL/91AGFvkwnMcqnK5pt63rk1/img.png)

    * ```java
      class TreeNode {
      	TreeNode left;			// 왼쪽 자식노드 : 부모노드의 값보다 작은 값
      	Object element;			// 객체를 저장하기 위한 참조변수
      	TreeNode right;			// 오른쪽 자식노드 : 부모 노드값보다 큰 값
      }
      ```

* TreeSet은 특히 이진 검색 트리의 성능을 향상시킨 **'레드-블랙 트리'** 로 구현되어 있음

* 자동 오름차순 정렬됨

* 중복 데이터 저장 X, 저장 순서 유지 X

* 사용법

  * ```java
    TreeSet<E> treeSet = new TreeSet<E>();
    ```

  * Set 인터페이스 타입 변수에 대입해도 됨

  * TreeSet 클래스 타입으로 대입한 이유

    * 객체를 찾거나 범위 검색과 관련된 메소드를 사용하기 위해서

#### 3-1. TreeSet이 가지고 있는 메소드

* **검색 관련 메소드**

  * | 리턴 타입 | 메소드 명    | 설명                                                         |
    | --------- | ------------ | ------------------------------------------------------------ |
    | E         | first()      | 제일 낮은 객체 리턴                                          |
    | E         | last()       | 제일 높은 객체 리턴                                          |
    | E         | lower(E e)   | 주어진 객체보다 바로 아래 객체 리턴                          |
    | E         | higher(E e)  | 주어진 객체보다 바로 위 객체 리턴                            |
    | E         | floor(E e)   | 주어진 객체와 동등한 객체가 있으면 리턴,<br />만약 없다면 주어진 객체 바로 아래의 객체를 리턴 |
    | E         | ceiling(E e) | 주어진 객체와 동등한 객체가 있으면 리턴,<br />만약 없다면 주어진 객체 바로 위의 객체를 리턴 |
    | E         | pollFirst()  | 제일 낮은 객체를 꺼내오고, 컬렉션에서 제거함                 |
    | E         | pollLast()   | 제일 높은 객체를 꺼내오고, 컬렉션에서 제거함                 |

* **정렬 관련 메소드**

  * | 리턴 타입         | 메소드 명            | 설명                                    |
    | ----------------- | -------------------- | --------------------------------------- |
    | Iterator< E >     | descendingIterator() | 내림차순으로 정렬된 Iterator를 리턴     |
    | NavigableSet< E > | descendingSet()      | 내림차순으로 정렬된 NavigableSet을 리턴 |

* **범위 검색 관련 메소드**

  * | 리턴 타입         | 메소드 명                                                    | 설명                                                         |
    | ----------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
    | NavigableSet< E > | headSet( E toElement, boolean inclusive )                    | 주어진 객체보다 낮은 객체들을 NavigableSet으로 리턴.<br />주어진 객체 포함 여부는 두 번째 파라미터에 따라 달라짐 |
    | NavigableSet< E > | tailSet( E fromElement, boolean inclusive )                  | 주어진 객체보다 높은 객체들을 NavigableSet으로 리턴.<br />주어진 객체 포함 여부는 두 번째 파라미터에 따라 달라짐 |
    | NavigableSet< E > | subSet( E fromElement, boolean frominclusive, E toElement, boolean toinclusive ) | 시작과 끝으로 주어진 객체 사이의 객체들을 NavigableSet으로 리턴.<br />시작과 끝 객체의 포함 여부는 두 번째, 네 번째 파라미터에 따라 달라짐 |


<br/>

* +) 수의 경우에는 크고 작음의 기준이 명확하지만, String name, int age 가 동시에 존재하는 경우에는 이름 오름차순인지, 나이 오름차순인지에 대한 기준을 프로그래머가 결정해야 함
  - Comparable<T\>을 사용하여 기준을 정함

* +) **인스턴스의 비교 기준을 정의하는 Comparable<T\> 인터페이스의 구현 기준**

  - Comparable<T\> 인터페이스를 구현할 때 정의해야 할 추상 메소드
    - `int compareTo(T o)`
    - 정의 방법
      - 인자로 전달된 o가 작다면 양의 정수 반환
      - 인자로 전달된 o가 크다면 음의 정수 반환
      - 인자로 전달된 o와 같다면 0을 반환
    - ex) `my.comareTo(your);`
      - your가 my 보다 작다면 양의 정수, 반대면 음의 정수를 반환하도록 구현
      - TreeSet<E\>는 compareTo 메소드의 호출결과를 바탕으로 정렬을 유지

  - 예제

    ```java
    import java.util.TreeSet;
    
    class Person implements Comparable<Person>{
        private String name;
        private int age;
    
        public Person(String name, int age){
            this.name = name;
            this.age = age;
        }
    
        @Override
        public String toString(){ return name + " : " + age; }
    
        @Override
        public int compareTo(Person p){
            return this.age - p.age; // 인자로 전달된 것이 크면 음수 --> 뒤로 배치
        }
    }
    
    public class ComparablePerson {
        public static void main(String[] args){
            TreeSet<Person> tree = new TreeSet<>();
            tree.add(new Person("YOON", 37));
            tree.add(new Person("HONG", 53));
            tree.add(new Person("PARK", 20));
    
            System.out.println(tree);
        }
    }
    ```

    ![img](https://github.com/fake-developers/1st/raw/JYJ-06/JYJ/resources/ComparablePerson.JPG)

    - 인자로 전달된 인스턴스의 나이가 더 많으면 음수가 반환됨

      - 정렬 순서상 뒤쪽에 위치하게 됨

    - 나이가 많은 사람을 앞으로 하고 싶으면 p.age - this.age 로 바꾸면 됨

      - 그러나 일시적인 기준 변경이라면 메소드를 수정하는 것보다 이러한 상황을 고려하여 제공되는 다음 인터페이스를 사용함

      - ```
        public interface Comparator<T>
        ```

        - `int compare(T o1, T o2)`

      - 이 인터페이스를 구현한 클래스의 인스턴스는 다음 생성자를 통해 전달할 수 있음

        - `public TreeSet(Comparator<? super E> comparator)`

      - 이렇게 생성된 TreeSet<E\>의 인스턴스는 생성자로 전달된 인스턴스의 compare 메소드의 호출 결과를 기준으로 정렬을 진행

        - o1 이 o2 보다 크면 양의 정수 반환
        - o1 이 o2 보다 작으면 음의 정수 반환
        - o1 이 o2 와 같으면 0 반환

<br/>

## :page_with_curl: Reference

[[JAVA] 컬렉션 프레임워크(Collection Framework) - (3)Set - Set 컬렉션 사용법](https://hijjang2.tistory.com/180)

[[Java] 컬렉션 프레임워크 - Set 컬렉션](https://palpit.tistory.com/entry/Java-컬렉션-프레임워크-Set-컬렉션)

[자바 - 컬렉션 프레임워크 : HashSet](https://doublesprogramming.tistory.com/184)

[자바/컬렉션 프레임워크 - Set 계열의 컬렉션(HashSet<E>, TreeSet<E>)](https://m.blog.naver.com/PostView.nhn?blogId=zag001&logNo=221536364274&proxyReferer=https:%2F%2Fwww.google.com%2F)

[[자바의 정석 3판] Chapter 11 컬렉션 프레임워크](https://m.blog.naver.com/kbeeysk/221780142868)

[[JAVA\] 컬렉션 프레임워크(Collection Framework) - (5)검색기능을 강화시킨 컬렉션 - TreeSet, TreeMap 사용법](https://hijjang2.tistory.com/182)
