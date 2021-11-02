# [JAVA] Stream(filter,map)

✍️ *Assembled by JiYoung-Kwon (2021-11-02)*

## 1. 스트림 (Stream)

* 자바8부터 Stream 사용 가능
* 자바 컬렉션/ 배열 원소 가공
  * 기존 : for문, foreach 등으로 원소를 하나씩 골라 가공
  * Stream : lambda 함수 형식으로 간결하고 깔끔하게 요소 처리 가능

1. filter : 요소들을 **조건에 따라 걸러내는** 작업을 해 줌
2. map : 요소들을 **특정 조건에 해당하는 값으로 변환** 해 줌
3. sorted : 요소들을 **정렬해주는 작업** 을 해 줌

+) 가공이 끝나면, 리턴해줄 결과를 collect를 통해 만들어준다.



## 2. 예제

* TEST SET

```java
ArrayList<string> list = new ArrayList<>(Arrays.asList("Apple","Banana","Melon","Grape","Strawberry"));

System.out.println(list);

//[Apple, Banana, Melon, Grape, Strawberry]
```

* **filter**

```java
//요소의 크기가 5 이상인 값만 뽑아내기
list.stream().filter(t->t.length()>5)
 
//예제
System.out.println(list.stream().filter(t->t.length()>5).collect(Collectors.joining(" "))); //Banana Strawberry

System.out.println(list.stream().filter(t->t.length()>5).collect(Collectors.toList())); //[Banana, Strawberry]
```

* **map**

```java
//리스트의 요소들을 대문자로 변경
list.stream().map(s->s.toUpperCase());
list.stream().map(String::toUpperCase);

//예제
System.out.println(list.stream().map(s->s.toUpperCase()).collect(Collectors.joining(" "))); //APPLE BANANA MELON GRAPE STRAWBERRY

System.out.println(list.stream().map(s->s.toUpperCase()).collect(Collectors.toList())); //[APPLE, BANANA, MELON, GRAPE, STRAWBERRY]
System.out.println(list.stream().map(String::toUpperCase).collect(Collectors.toList())); //[APPLE, BANANA, MELON, GRAPE, STRAWBERRY]

list.stream().map(String::toUpperCase).forEach(s -> System.out.println(s));
//APPLE
//BANANA
//MELON
//GRAPE
//STRAWBERRY
//+) forEach 요소마다 각각 작업 가능
```

* **sorted**

```java
//list의 요소를 정렬
list.stream().sorted()
    
System.out.println(list.stream().sorted().collect(Collectors.toList()));
//[Apple, Banana, Grape, Melon, Strawberry]

```

+) Stream에 대한 자세한 내용은 [여기](https://futurecreator.github.io/2018/08/26/java-8-streams-advanced/)를 참고



## 📃 Reference

* [[Java]자바 스트림Stream(map,filter,sorted / collect,foreach)](https://dpdpwl.tistory.com/81)

* [Java 1.8 컬렉션 stream, filter, map, foreach, sort](https://lts0606.tistory.com/157)

* [Java 스트림(map, filter, sorted / collect, foreach)](https://velog.io/@coffiter/Java-%EC%8A%A4%ED%8A%B8%EB%A6%BCmap-filter-sorted-collect-foreach)
