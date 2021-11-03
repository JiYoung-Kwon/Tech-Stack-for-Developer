# [JAVA] Optional

✍️ *Assembled by JiYoung-Kwon (2021-11-03)*

## 1. NPE

* NullPointerException

* 개발 시 가장 많이 발생하는 예외 중 하나

* NPE를 피하기 위해선 null을 검사하는 로직을 추가해야 함

  * null 검사 변수가 많은 경우, 코드 복잡도 증가&로직 번거로움
  * 따라서 null대신 초기값 사용을 권장하기도 함

* ```java
  List<String> names = getNames();
  names.sort(); // names가 null이라면 NPE가 발생함
   
  List<String> names = getNames();
  // NPE를 방지하기 위해 null 검사를 해야함
  if(names != null){
      names.sort();
  }
  ```



## 2. Optional

* JAVA8에서 사용 가능

* Optional<T\>클래스를 사용해 NPE를 방지할 수 있도록 함

  * null이 올 수 있는 값을 감싸는 Wrapper 클래스

  * 참조하더라도 NPE가 발생하지 않도록 도와줌

  * ```java
    public final class Optional<T> {
     
      // If non-null, the value; if null, indicates no value is present
      private final T value;
       
      ...
    }
    ```

  * 위와 같은 value에 값을 저장하기 떄문에, null이더라도 바로 NPE가 발생하지 않음

  * 각종 메소드를 제공해줌

* 참고

  * 값을 Wrapping하고 풀고, null일 경우 대체 함수 호출 등의 오버헤드가 있어 성능이 저하될 수 있음
  * 메소드의 반환 값이 절대 null이 아니라면 Optional을 사용하지 않는 것이 성능저하가 적음
  * 즉, 메소드의 결과가 null이 될 수 있으며, 클라이언트가 상황을 처리해야할 때 사용

* 



## 3. 활용

##### Optional 생성

- 빈 객체 생성
  - ```java
    Optional<String> optional = Optional.empty();
    
    System.out.println(optional); //Optional.empty
    System.out.println(optional.isPresent()); //false
    ```

- 어떤 데이터가 null이 올 수 있는 경우 -> 해당 값 Optional로 감싸기

  - ```java
    // Optional의 value는 값이 있을 수도 있고 null 일 수도 있음
    Optional<String> optional = Optional.ofNullable(getName());
    String name = optional.orElse("anonymous"); // 값이 없다면 "anonymous" 를 리턴
    ```

##### Optional 사용

* ```java
  // Java8 이전(기존)
  List<String> names = getNames();
  List<String> tempNames = list != null ? list : new ArrayList<>();
   
  //Optional<T>, Lambda 이용
  List<String> nameList = Optional.ofNullable(getList()).orElseGet(() -> new ArrayList<>());
  ```

##### 활용 예시1

* ```java
  // 기존 우편번호 null 검사 코드
  UserVO userVO = getUser();
  if (userVO != null) {
    Address address = user.getAddress();
    if (address != null) {
      String postCode = address.getPostCode();
      if (postCode != null) {
        return postCode;
      }
    }
  }
  return "우편번호 없음";
  
  // 위의 코드를 Optional로 펼쳐놓은 것
  Optional<UserVO> userVO = Optional.ofNullable(getUser());
  Optional<Address> address = userVO.map(UserVO::getAddress);
  Optional<String> postCode = address.map(Address::getPostCode);
  String result = postCode.orElse("우편번호 없음");
   
  // 축약ver
  String result = user.map(UserVO::getAddress)
      .map(Address::getPostCode)
      .orElse("우편번호 없음");
  ```



##### 활용 예시2

* ```java
  // 기존 코드 NPE 처리
  String name = getName();
  String result = "";
   
  try {
    result = name.toUpperCase();
  } catch (NullPointerException e) {
    throw new CustomUpperCaseException();
  }
  
  // Optional 활용
  Optional<String> nameOpt = Optional.ofNullable(getName());
  String result = nameOpt.orElseThrow(CustomUpperCaseExcpetion::new).toUpperCase();
  ```



## 3. orElse vs orElseGet

* orElse

  * Optional 안의 값이 null이든 아니든 항상 호출됨
  * 그에 따른 비용이 추가되고, 문제가 발생할 수 있음
  * 값이 미리 존재하는 경우 사용

* orElseGet

  * Optional 안의 값이 null일 경우에만 호출됨
  * 비용이 orElse보다 저렴, 불필요한 문제 발생 X
  * 값이 미리 존재하지 않는 거의 대부분의 경우 사용

* ```java
  public void findUserEmail() {
      String userEmail = "Empty";
      String result1 = Optional.ofNullable(userEmail).orElse(getUserEmail());
      System.out.println(result1);
   
      userEmail = "Empty";
      String result2 = Optional.ofNullable(userEmail).orElseGet(this::getUserEmail);
      System.out.println(result2);
  }
   
  private String getUserEmail() {
      System.out.println("getUserEmail() Called");
      return "userEmail@gmail.com";
  }
   
  //getUserEmail() Called
  //Empty
   
  //Empty
  ```

* 

## 📃 Reference

* [[Java] Optional이란?](https://mangkyu.tistory.com/70)
* [Optional 클래스](http://tcpschool.com/java/java_stream_optional)
* [[Java] Optional이란?](https://esoongan.tistory.com/95) 
