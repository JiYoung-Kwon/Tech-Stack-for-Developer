# [JAVA] 컬렉션 프레임워크 - Map 컬렉션

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

## 1. Map 컬렉션

* HashMap, Hashtable, Properties, TreeMap 등이 있음
* Set과 같은 **비선형 자료구조**
* 키(Key)를 값(Value)에 매핑(Mapping)하는 기능을 제공함
  * **키가 중복되지 않는다면** 똑같은 **값을 중복으로 적재할 수 있음**
  * 동일한 키를 등록할 수 없고, 유일해야 하며, 각 키는 한 개의 값만을 매핑해야 함
  * 키와 값은 모두 객체임
  * 기존에 저장된 키와 동일한 키로 값을 저장하면, 기존의 값은 없어지고 새로운 값으로 대치됨
  * ![img](https://t1.daumcdn.net/cfile/tistory/275CB23B55F525B617)

#### 1-1.  Map 인터페이스 메소드

* 키로 객체들을 관리하기 때문에, 키를 파라미터로 갖는 메소드가 많음

* ![img](https://t1.daumcdn.net/cfile/tistory/2248C83B55F525B82B)

  * 매개 변수 타입과 리턴 타입에 K와 V라는 타입 파라미터가 있음

    * Map 인터페이스가 제네릭 타입이기 때문
    * 구체적인 타입은 구현 객체를 생성할 때 결정됨

  * 사용법

    * ```java
      Map<String, Integer> map = new HashMap<String,Integer>();
      
      map.put("Jackie",30);				//객체 추가
      int score = map.get("Jackie");		//객체 검색
      System.out.println(score);
      
      map.remove("Jackie");				//객체 삭제
      ```

* 저장된 전체 객체를 대상으로 하나씩 객체를 얻고 싶은 경우

  1. 첫 번째 방법

     1. keySet() 메소드로 모든 키를 Set 컬렉션으로 얻음
     2. 반복자를 통해 키를 하나씩 얻음
     3. get() 메소드를 통해 값을 얻음

     ```java
     Map<K, V> map = ~;						//생략
      
     Set<K> keySet = map.keySet();
     Iterator<K> it = keySet.iterator();
      
     while (it.hasNext()) {
         K key = it.next();
         V value = map.get(key);
     }
     ```

  2. 두 번째 방법

     1. entrySet() 메소드로 모든 Map.Entry를 Set 컬렉션으로 얻음
     2. 반복자를 통해 Map.Entry 객체를 하나씩 얻음
     3. getKey()와 getValue() 메소드를 이용해 키와 값을 얻음

     ```java
     Set<Map.Entry<K, V>> entrySet = map.entrySet();
      
     Iterator<Map.Entry<K, V>> entryIt = entrySet.iterator();
      
     while (entryIt.hasNext()) {
         Map.Entry<K, V> entry = entryIt.next();
      
         K key = entry.getKey();
         V value = entry.getValue();
     }
     ```

<br/>


## 2. HashMap

* Map 인터페이스의 구현 클래스

* HashMap의 키로 사용할 객체는 hashCode()와 equals() 메소드를 재정의해서 동등 객체가 될 조건을 정해야 함

  * 동등 객체가 될 조건
    * hashCode()의 리턴 값이 같아야 함
    * equals() 메소드가 true를 리턴해야 함

* 주로 키 타입은 String을 많이 사용함

  * String은 문자열이 같을 경우, 동등 객체가 될 수 있도록 hashCode()와 equals() 메소드가 재정의되어 있음

* 사용법

  * ```java
    Map<K,V> map = new HashMap<K,V>(); //기본 생성자 호출
    ```

  * 키 타입과 값 타입을 파라미터로 주고, 기본 생성자를 호출

  * 키, 값 타입

    * 기본 타입(boolean, char, byte, short, int, long, float, double)을 사용할 수 없음
    * **클래스 및 인터페이스 타입만** 가능

#### 2-1. 예시

1. 이름을 키로, 점수를 값으로 저장하는 HashMap 사용 예제

* **HashMapExam.java**

  * ```java
    package set;
     
    import java.util.HashMap;
    import java.util.Iterator;
    import java.util.Map;
    import java.util.Set;
     
    public class HashMapExam {
     
        public static void main(String[] args) {
            Map<String, Integer> map = new HashMap<String, Integer>();
            
            map.put("Jack", 30);
            map.put("Andy", 40);
            map.put("John", 22);
            map.put("Jolie", 10);
            map.put("Exo", 50);
            map.put("Tiger", 91);
            
            System.out.println("총 Entry 수: " + map.size());
            
            System.out.println("\tJolie" + map.get("Jolie"));
            System.out.println();
            
            // 객체를 하나씩 처리
            Set<String> keySet = map.keySet();
            Iterator<String> it = keySet.iterator();
            
            while (it.hasNext()) {
                String key = it.next();
                Integer value = map.get(key);
                System.out.println("\t" + key + " : " + value);
            }
            
            System.out.println();
            
            // 객체 삭제
            map.remove("Exo");
            System.out.println("총 Entry 수: " + map.size());
            
            map.clear();
            System.out.println("총 Entry 수: " + map.size());
        }
    }
    ```

* **결과**

  * ![img](https://t1.daumcdn.net/cfile/tistory/2768863B55F525BA0D)

2. 사용자 정의 객체인 Student를 키로하고 점수를 저장하는 HashMap 사용 예제

* **Student.java**

  * ```java
    package set;
     
    public class Student {
        public int sno;
        public String name;
     
        public Student(int sno, String name) {
            super();
            this.sno = sno;
            this.name = name;
        }
     
        @Override
        public boolean equals(Object obj) {
            if (obj instanceof Student) {
                Student std = (Student) obj;
     
                return (sno == std.sno) && (name == std.name);
            } else {
                return false;
            }
        }
     
        @Override
        public int hashCode() {
            return sno + name.hashCode();
        }
    }
    ```

* **HashMapExam2.java**

  * ```java
    package set;
     
    import java.util.HashMap;
    import java.util.Map;
     
    public class HashMapExam2 {
     
        public static void main(String[] args) {
            Map<Student, Integer> map = new HashMap<Student, Integer>();
     
            map.put(new Student(1, "Jolie"), 100);
            map.put(new Student(1, "Jolie"), 100);
     
            System.out.println("총 Entry 수: " + map.size());
        }
    }
    ```

* 결과

  * ![img](https://t1.daumcdn.net/cfile/tistory/216AE63B55F525BC0B)

<br/>

## 3. Hashtable

* HashMap과 **동일한 내부 구조** 를 가짐
* 키로 사용할 객체는 hashCode()와 equals() 메소드를 재정의해서 동등 객체가 될 조건을 정해야 함
* **HashMap과의 차이점**
  * Hashtable은 **동기화된(Synchronized) 메소드로 구성** 되어 있음
    * 멀티 스레드가 동시에 이 메소드들을 실행할 수 없음
    * 하나의 스레드가 실행을 완료해야만 다른 스레드를 실행할 수 있음
  * 따라서, **멀티 스레드 환경에서 안전하게 객체를 추가, 삭제할 수 있음**
  * ![img](https://t1.daumcdn.net/cfile/tistory/245DBE4855F6410732)

* 사용법

  * ```java
    Map<K,V> map = new Hashtable<K,V>(); //기본 생성자 호출
    ```

  * 키 타입과 값 타입을 파라미터로 주고, 기본 생성자를 호출

#### 3-1. 예시

1. 키보드로 아이디와 비밀번호를 입력받아서, Hashtable에 저장되어 있는 키(아이디)와 값(비밀번호)으로 비교한 후 로그인 여부를 출력하는 예제

* **HashtableExam.java**

  * ```java
    package set;
     
    import java.util.Hashtable;
    import java.util.Map;
    import java.util.Scanner;
     
    public class HashtableExam {
        
        public static void main(String[] args) {
            Map<String, String> map = new Hashtable<String, String>();
     
            map.put("ABC", "123");
            map.put("DEF", "456");
            map.put("GHI", "789");
     
            Scanner scan = new Scanner(System.in);
     
            while (true) {
                System.out.println("아이디와 비밀번호를 입력해주세요.");
                System.out.print("아이디: ");
                String id = scan.nextLine();
     
                System.out.print("비밀번호: ");
                String pwd = scan.nextLine();
                System.out.println();
     
                if (map.containsKey(id)) {
                    if (map.get(id).equals(pwd)) {
                        System.out.println("로그인되었습니다.");
                        break;
                    } else {
                        System.out.println("비밀번호가 일치하지 않습니다.");
                    }
                } else {
                    System.out.println("입력하신 아이디가 존재하지 않습니다.");
                }
            }
            scan.close();
        }
    }
    ```

* **결과**

  * ![img](https://t1.daumcdn.net/cfile/tistory/2176E74855F6410A1E)



## 4. Properties

* properties는 Hashtable의 하위 클래스임

  * Hashtable의 모든 특징을 그대로 가지고 있음
  * **차이점**
    * Hashtable : 키와 값을 **다양한 타입으로 지정이 가능**
    * Properties : 키와 값을 **String 타입으로 제한한 컬렉션**

* 애플리케이션의 옵션 정보, 데이터베이스 연결 정보, 국제화(다국어) 정보가 저장된 **프로퍼티(*.properties) 파일** 을 읽을 때 주로 사용

  * 프로퍼티 파일 : 키와 값이 = 기호로 연결되어 있는 텍스트 파일
    * ISO 8859-1 문자셋으로 저장됨
    * 이 문자셋으로 직접 표현할 수 없는 한글은 유니코드로 변환되어 저장됨

  * 프로퍼티 파일 내용 예시

    * ```properties
      driver=oracle.jdbc.OracleDriver
      url=jdbc:oracle:thin:@localhost:1521:orcl
      username=scott
      password=tiger
      ```

    * driver, url, username, password는 키, 그 뒤의 문자열은 값이 됨

* **프로퍼티 파일 읽기**

  * ```java
    Properties properties = new Properties(); //Properties 객체 생성
     
    properties.load(new FileReader("C:/~/database.properties"));
    ```

  * load() 메소드 : 프로퍼티 파일로부터 데이터를 읽기 위해 FileReader 객체를 파라미터로 받음

  * 프로퍼티 파일은 일반적으로 클래스 파일과 함께 저장

    * 경로 얻어오기 : Class의 getResource() 메소드 이용

    * ```java
      String path = PropertiesExam.class.getResource("database.properties").getPath();
      //클래스 파일과 동일한 위치에 있는 프로퍼티 파일 읽어오기
      
      path = URLDecoder.decode(path, "utf-8");
      ```

  * 프로퍼티 객체에서 해당 키의 값 얻기 : getProperty() 메소드 사용

<br/>

## 5. TreeMap

* 이진 트리 구조를 기반으로 한 Map 컬렉션

* **TreeSet과의 차이점**

  * 키와 값이 저장된 Map.Entry를 저장한다는 점

* TreeMap에 객체를 저장하면 자동으로 정렬됨
  * 기본적으로 부모 키 값과 비교해서 낮은 것은 왼쪽 노드, 높은 것은 오른쪽 노드에 저장


  * ![img](https://blog.kakaocdn.net/dn/bwrp1O/btqAMPwRawM/DtIqeFfeW4N0vXCHjBA2NK/img.png)

* 사용법

  * ```java
    TreeMap<K,V> treeMap = new TreeMap<K,V>();
    ```

  * Map 인터페이스 타입 변수에 대입해도 됨

  * TreeMap 클래스 타입으로 대입한 이유

    * 특정 객체를 찾거나 범위 검색과 관련된 메소드를 사용하기 위해서

#### 5-1. TreeMap이 가지고 있는 메소드

* **검색 관련 메소드**

  * | 리턴 타입      | 메소드 명           | 설명                                                         |
    | -------------- | ------------------- | ------------------------------------------------------------ |
    | Map.Entry<K,V> | firstEntry()        | 제일 낮은 Map.Entry 리턴                                     |
    | Map.Entry<K,V> | lastEntry()         | 제일 높은 Map.Entry 리턴                                     |
    | Map.Entry<K,V> | lowerEntry(K key)   | 주어진 객체보다 바로 아래 Map.Entry 리턴                     |
    | Map.Entry<K,V> | higherEntry(K key)  | 주어진 객체보다 바로 위 Map.Entry 리턴                       |
    | Map.Entry<K,V> | floorEntry(K key)   | 주어진 객체와 동등한 키가 있으면 해당 Entry 리턴,<br />만약 없다면 주어진 키 바로 아래의 Entry를 리턴 |
    | Map.Entry<K,V> | ceilingEntry(K key) | 주어진 객체와 동등한 키가 있으면 해당 Entry 리턴,<br />만약 없다면 주어진 객체 바로 위의 Entry를 리턴 |
    | Map.Entry<K,V> | pollFirstEntry()    | 제일 낮은 Entry를 꺼내오고, 컬렉션에서 제거함                |
    | Map.Entry<K,V> | pollLastEntry()     | 제일 높은 Entry를 꺼내오고, 컬렉션에서 제거함                |

* **범위 검색 관련 메소드**

  * | 리턴 타입         | 메소드 명                                                    | 설명                                                         |
    | ----------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
    | NavigableMap<K,V> | headMap( K toKey, boolean inclusive )                        | 주어진 키보다 낮은 Map.Entry들을 NavigableMap으로 리턴.<br />주어진 키의 Map.Entry 포함 여부는 두 번째 파라미터에 따라 달라짐 |
    | NavigableMap<K,V> | tailMap( K fromKey, boolean inclusive )                      | 주어진 키보다 높은 Map.Entry들을 NavigableMap으로 리턴.<br />주어진 키의 Map.Entry 포함 여부는 두 번째 파라미터에 따라 달라짐 |
    | NavigableMap<K,V> | subMap( K fromKey, boolean frominclusive, K toKey, boolean toinclusive ) | 시작과 끝으로 주어진 키 사이의 Map.Entry들을 NavigableMap으로 리턴.<br />시작과 끝 키의 Map.Entry 포함 여부는 두 번째, 네 번째 파라미터에 따라 달라짐 |

    


<br/>

## :bulb: 예상질문

<br/>

## :page_with_curl: Reference

[컬렉션 프레임워크 (Collection Framework) - 3 (set, map)](https://lipcoder.tistory.com/entry/%EC%BB%AC%EB%A0%89%EC%85%98-%ED%94%84%EB%A0%88%EC%9E%84%EC%9B%8C%ED%81%AC-Collection-Framework-3-set-map)

[[JAVA] 컬렉션 프레임워크 - Map 컬렉션](https://palpit.tistory.com/656)

[자바 컬렉션 프레임워크(Collection Framework)Map 컬렉션(HashMap, Hashtable)](https://lsjsj92.tistory.com/62?category=753578)

[자바/컬렉션 프레임워크 - Map 계열의 컬렉션(HashMap<K, V>, Properties<K, V>)](https://m.blog.naver.com/zag001/221536421906)

[[자바의 정석 3판] Chapter 11 컬렉션 프레임워크](https://m.blog.naver.com/kbeeysk/221780142868)

[[JAVA] 컬렉션 프레임워크(Collection Framework) - (5)검색기능을 강화시킨 컬렉션 - TreeSet, TreeMap 사용법](https://hijjang2.tistory.com/182)
