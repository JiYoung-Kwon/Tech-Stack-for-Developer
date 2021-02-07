# [DATA STRUCTURE] 스택(Stack), 큐(Queue)

:writing_hand: *Assembled by JiYoung-Kwon (2021-01-26)* 



## 1. 스택(Stack)

<img src =https://blog.kakaocdn.net/dn/by1qnT/btqBE1v1UlX/zbnXdYnGAXhMYbcDCca6WK/img.png width = 50%>

* 쌓아 올린다는 것을 의미
* 차곡차곡 쌓아 올린 형태의 자료구조

#### 1-1. 특징

* **LIFO 구조** : 후입선출(Last-in First-out)
  * 마지막에 들어온 것이 먼저 나간다
  * 입구와 출구가 같은 자료구조
* 같은 구조와 크기의 자료를 정해진 방향으로만 쌓을 수 있음
* top으로 정한 곳을 통해서만 접근할 수 있음, 자료 삭제 또한 top을 통해서만 가능
* **top** : 가장 위에 있는 자료, 가장 최근에 들어온 자료
  * 삽입되는 새 자료는 top이 가리키는 자료의 위에 쌓이게 됨
  * 초기값 : -1
* **push** : top을 통해 삽입하는 연산
* **pop** : top을 통해 삭제하는 연산
* 예외 처리
  * stack underflow : 비어있는 스택에서 원소를 추출하려 할 때
  * stack overflow : 스택이 넘치는 경우

#### 1-2. 활용 예시

* 웹 브라우저 방문기록 (뒤로 가기) : 가장 나중에 열린 페이지부터 다시 보여준다.

* 역순 문자열 만들기 : 가장 나중에 입력된 문자부터 출력한다.

* 실행 취소 (undo) : 가장 나중에 실행된 것부터 실행을 취소한다.

* 후위 표기법 계산

* 수식의 괄호 검사 (연산자 우선순위 표현을 위한 괄호 검사)

#### 1-3. 오퍼레이션

* isEmpty() : 스택이 현재 비어있는지 체크

* push(data) : 스택에 데이터 삽입

* pop() : 스택에서 데이터 삭제

* peek() : 스택의 맨 위(다음에 꺼낼 데이터) 확인

#### 1-4. 구현

```java
import java.util.EmptyStackException;
 
public class Stack {
    
    private static class Node {
        private int data;
        private Node next;
        private Node(int data) {
            this.data = data;
        }
    }
    
    private Node top;
    
    public boolean isEmpty() {
        return top == null;
    }
    
    public int peek() {
        if(isEmpty()) throw new EmptyStackException();
 
        return top.data;
    }
    
    public void push(int data) {
        Node node = new Node(data);
        node.next = top;
        top = node;
    }
    
    public int pop() {
        if(isEmpty()) throw new EmptyStackException();
        
        int data = top.data;
        top = top.next;
        return data;
    }
}
```



<br/>

## 2. 큐(Queue)

<img src = https://blog.kakaocdn.net/dn/Zce3U/btqBDaOfGU5/Rc2kR3Puqi3QiQa3o6CPL1/img.png width = 50%>

* 줄 or 줄을 서서 기다리는 것

#### 2-1. 특징

* **FIFO 구조** : 선입선출(First-in First-out)
  * 먼저 들어온 것이 먼저 나간다
  * 공연장에서 입장을 기다리는 관객
* 한 쪽 끝에서 삽입 작업, 다른 쪽 끝에서 삭제 작업이 양쪽으로 이루어짐
  * **front** : 삭제연산만 수행되는 곳. 첫 원소
  * **rear** : 삽입연산만 수행되는 곳. 끝 원소
* **deQueue** : 데이터의 삭제 연산. front에서 이루어짐
* **enQueue** : 데이터의 삽입 연산. rear에서 이루어짐
* 들어올 때 rear로 들어오지만 나올 때는 front부터 빠지는 특성

![img](https://blog.kakaocdn.net/dn/d5LoA5/btqv2J2pRWI/Kp4ZssKzbhVPWxcKnHUww0/img.png)

#### 2-2. 활용 예시

주로 데이터가 입력된 시간 순서대로 처리해야 할 필요가 있는 상황에 이용

* 우선순위가 같은 작업 예약 (프린터의 인쇄 대기열)
* 은행 업무
* 콜센터 고객 대기시간
* 프로세스 관리
* 너비 우선 탐색(BFS, Breadth-First Search) 구현
* 캐시(Cache) 구현

#### 2-3. 문제점

일반적으로 배열을 `[1] [2] [3] [4] [5]` 이런 직선 형태로 보았을 때, 

가장 오래 기다린, 처음 들어온 [1]이라는 데이터가 Pop이 되면

다른 데이터들을 차례대로 땡겨주어야 한다. [Pop] [2] [3] [4] [5]

* Dequeue가 되면 Dequeue된 자리를 채우기 위해 rear에서 front까지 자리이동을 해줘야 함

* 소수의 자료의 경우는 상관이 없지만 많은 데이터의 경우 연산에 많은 시간이 걸림

-> 이러한 문제점을 해결하기 위해 나온 것이 **원형 큐, 순환 큐, 환영 큐**라고 불리는 방법

![img](https://t1.daumcdn.net/cfile/tistory/195258464E7ECB1C0D)

* 배열을 직선으로 보는게 아니라 원형으로 보는 방법

#### 2-4. 오퍼레이션

* isEmpty() : 큐가 현재 비어있는지 체크
* enqueue() : 큐에 데이터 삽입
* dequeue() : 큐에서 데이터 삭제
* peek() : 큐의 맨 앞(다음에 꺼낼 데이터) 확인

#### 2-5. 구현

```java
import java.util.EmptyStackException;
 
public class Queue {
    
    private static class Node{
        private int data;
        private Node next;
        private Node(int data) {
            this.data = data;
        }
    }
    
    private Node front;
    private Node rear;
    
    public boolean isEmpty() {
        return front == null;
    }
    
    public int peek() {
        return front.data;
    }
    
    public void enqueue(int data) {
        Node node = new Node(data);
        if(rear != null) {
            rear.next = node;
        }
        rear = node;
        if(front == null) {
            front = node;
        }
    }
    
    public int dequeue() {
        if(isEmpty()) throw new EmptyStackException();
        
        int data = front.data;
        front = front.next;
        if(front == null) {
            rear = null;
        }
        return data;
    }
}
```



<br/>

## 3. 스택 vs 큐

![img](https://blog.kakaocdn.net/dn/bktDKx/btqv0WVtpR8/3bv4drx1JRxMULKvQkjItK/img.png)

* 스택, 큐 java 코드 및 실행 결과

  ![img](https://blog.kakaocdn.net/dn/cUGGqC/btqBFMLWGSo/l6PWcEtBSbaeTMhZEB1q1K/img.png)

  ![img](https://blog.kakaocdn.net/dn/clpBnz/btqBE044p0k/zg7cblvKSBWkkoK032NV3k/img.png)

<br/>

## :page_with_curl: Reference

[[자료구조]스택과 큐. (stack and queue)](https://winplz.tistory.com/entry/%EC%9E%90%EB%A3%8C%EA%B5%AC%EC%A1%B0%EC%8A%A4%ED%83%9D%EA%B3%BC-%ED%81%90-stack-and-queue)

[[자료구조] 스택(Stack)과 큐(Queue) 이해하기](https://brightwon.tistory.com/8)

[[자료구조] 스택 (STACK), 큐(QUEUE) 개념/비교 /활용 예시](https://devuna.tistory.com/22)

[스택&큐 Stack and Queue 구현 java](https://beccacatcheserrors.tistory.com/41)
