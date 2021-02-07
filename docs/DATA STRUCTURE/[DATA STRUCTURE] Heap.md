# [DATA STRUCTURE] Heap

:writing_hand: *Assembled by JiYoung-Kwon (2021-01-31)* 



## 1. Heap이란?

- **우선순위 큐**를 위해 만들어진 자료구조

  > **우선순위 큐**
  >
  > - 우선순위의 개념에 큐를 도입한 자료구조
  > - 데이터들이 우선순위를 가지고 있고, 우선순위가 높은 데이터가 먼저 나감
  >
  > |          자료 구조          |        삭제되는 요소        |
  > | :-------------------------: | :-------------------------: |
  > |         스택(Stack)         |  가장 최근에 들어온 데이터  |
  > |          큐(Queue)          |   가장 먼저 들어온 데이터   |
  > | 우선순위 큐(Priority Queue) | 가장 우선순위가 높은 데이터 |
  >
  > - 이용 사례
  >
  >   - 시뮬레이션 시스템
  >   - 네트워크 트래픽 제어
  >   - 운영체제에서의 작업 스케줄링
  >   - 수치 해석적인 계산
  >
  > - 우선순위 큐는 배열, 연결리스트, 힙으로 구현 가능
  >
  >   - **힙으로 구현하는 것이 가장 효율적**
  >
  >      | 우선순위 큐를 구현하는 표현 방법 |     삽입     |     삭제     |
  >      | :------------------------------: | :----------: | :----------: |
  >      |          순서 없는 배열          |     O(1)     |     O(n)     |
  >      |      순서 없는 연결 리스트       |     O(1)     |     O(n)     |
  >      |           정렬된 배열            |     O(n)     |     O(1)     |
  >      |        정렬된 연결 리스트        |     O(n)     |     O(1)     |
  >      |           **힙(heap)**           | **O(log n)** | **O(log n)** |
  >
  >     

- **완전 이진 트리**의 일종

- 최댓값과 최솟값을 빠르게 찾아내도록 만들어진 자료구조

- 일종의 **반정렬 상태(느슨한 정렬 상태)**를 유지

  - 큰 값이 상위 레벨에 있고, 작은 값이 하위 레벨에 있다는 정도
  
  - 부모 노드의 키 값이 자식 노드의 키 값보다 항상 큰 (작은) 이진 트리를 말함
  
* 힙 트리에서는 중복된 값을 **허용**함 (이진 탐색 트리에서는 허용하지 않음)

<br/>

## 2. Heap의 종류

* 최대 힙(max heap)
  * 부모 노드의 키 값이 자식 노드의 키 값보다 크거나 같은 완전 이진 트리
  * key(부모 노드) >= key(자식 노드)
* 최소 힙(min heap)
    * 부모 노드의 키 값이 자식 노드의 키 값보다 작거나 같은 완전 이진 트리
    * key(부모 노드) <= key(자식 노드)
* ![img](https://gmlwjd9405.github.io/images/data-structure-heap/types-of-heap.png)

<br/>

## 3. Heap의 구현

* 힙을 저장하는 표준적인 자료구조 : **배열**
* 구현을 쉽게 하기 위하여 배열의 첫 번째 인덱스인 0은 사용되지 않음
* 특정 위치의 노드 번호는 새로운 노드가 추가되어도 변하지 않음
  * ex) 루트 노드의 오른쪽 노드의 번호는 항상 3이다.
* 힙에서의 부모 노드와 자식 노드의 관계
  * 왼쪽 자식의 인덱스 = (부모의 인덱스) * 2
  * 오른쪽 자식의 인덱스 = (부모의 인덱스) * 2 + 1
  * 부모의 인덱스 = (자식의 인덱스) / 2
* ![img](https://gmlwjd9405.github.io/images/data-structure-heap/heap-index-parent-child.png)

## 4. Heap의 삽입

1. 힙에 새로운 요소가 들어오면, 일단 새로운 노드를 힙의 마지막 노드에 이어서 삽입함

2. 새로운 노드를 부모 노드들과 교환해서 힙의 성질을 만족시킴


* 예시
   * 아래의 최대 힙(max heap)에 새로운 요소 8을 삽입
   * ![img](https://gmlwjd9405.github.io/images/data-structure-heap/maxheap-insertion.png)
   
* 구현

   ```java
   /* 최대힙 삽입 */
   void insert_max_heap(int x){
   	maxHeap[++heapSize] = x; // 힙 크기를 하나 증가하고 마지막 노드에 x를 넣는다.
   
   	for (int i=heapSize; i>1; i/=2){
     	// 마지막 노드가 자신의 부모 노드보다 크면 swap
     		if (maxHeap[i/2] < maxHeap[i]){
      			swap(i/2, i);
     		} 
           else{
       		break;
     		}
   	}
   }
   ```

## 5. Heap의 삭제

1. 최대 힙에서 최댓값은 루트 노드이므로 루트 노드가 삭제됨
   * 최대 힙(max heap)에서 삭제 연산은 최댓값을 가진 요소를 삭제하는 것
2. 삭제된 루트 노드에는 힙의 마지막 노드를 가져옴
3. 힙을 재구성함

* 예시

  * 아래의 최대 힙(max heap)에서 최댓값을 삭제
  * ![img](https://gmlwjd9405.github.io/images/data-structure-heap/maxheap-delete.png)

* 구현

  ```java
  /* 최대힙 삭제 */
  int delete_max_heap(){
  	if (heapSize == 0) // 배열이 빈 경우
    		return 0;
  
  	int item = maxHeap[1]; // 루트 노드의 값을 저장한다.
  	maxHeap[1] = maxHeap[heapSize]; // 마지막 노드의 값을 루트 노드에 둔다.
  	maxHeap[heapSize--] = 0; // 힙 크기를 하나 줄이고 마지막 노드를 0으로 초기화한다.
  
  	for (int i=1; i*2<=heapSize;) {
    		// 마지막 노드가 왼쪽 노드와 오른쪽 노드보다 크면 반복문을 나간다.
    		if (maxHeap[i] > maxHeap[i*2] && maxHeap[i] > maxHeap[i*2+1]) {
      		break;
    		}
    		// 왼쪽 노드가 더 큰 경우, 왼쪽 노드와 마지막 노드를 swap
    		else if (maxHeap[i*2] > maxHeap[i*2+1]) {
      		swap(i, i*2);
      		i = i*2;
    		}
    		// 오른쪽 노드가 더 큰 경우, 오른쪽 노드와 마지막 노드를 swap
    		else {
      		swap(i, i*2+1);
      		i = i*2+1;
    		}
  	}
  	return item;
  }
  ```

<br/>

## :bulb: 예상질문

Q1 - 자료구조에서 힙이 무엇인가요?

A1 - 우선순위 큐를 위해 만들어진 자료구조로, 최댓값과 최솟값을 빠르게 찾아내도록 만들어졌으며 완전 이진 트리의 형태를 가집니다.

<br/>

Q2 - 힙에 어떤 종류가 있나요?

A2 - 최대 힙과 최소 힙이 있습니다. 최대 힙은 부모 노드의 키 값이 자식 노드의 키 값보다 크거나 같은 완전 이진 트리이고, 최소 힙은 부모 노드의 키 값이 자식 노드의 키 값보다 작거나 같은 완전 이진 트리입니다.

<br/>

## :page_with_curl: Reference

[[자료구조] 힙(heap)이란](https://gmlwjd9405.github.io/2018/05/10/data-structure-heap.html)

[힙(Heap) 자료구조](https://www.crocus.co.kr/1184)

[자료구조 - 힙(Heap)이란?](https://galid1.tistory.com/485)