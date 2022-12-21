# 연결리스트

- 연결리스트는 각 요소를 포인터로 연결하여 관리하는 선형 자료구조다.
- 각 요소는 노드라고 부르며 데이터 영역과 포인터 영역으로 구성된다.

## 연결리스트의 특징

- 메모리가 허용하는 한 요소를 제한없이 추가할 수 있다.
- 탐색은 O(n)이 소요된다.
- 요소를 추가하거나 제거할 때는 O(1)이 소요된다.
- Singly Linked List, Doubly Linked List, Circular Linked List가 존재한다.

## 배열과 차이점

- 메모리 차이(배열은 메모리 영역을 연속적으로 사용하지만 연결리스트는 퍼져있다.)
- 배열 요소 삭제 : O(n) / 연결리스트 요소 삭제 : O(1)
- 배열 요소 추가 : O(n) / 연결리스트 요소 추가 : O(1)

## Singly Linked List

- Head에서 Tail까지 단방향으로 이어지는 연결 리스트
- 가장 단순한 형태인 연결 리스트이다.

### 요소 찾기

- O(n) 소요

### 요소 추가

- O(1) 소요

### 요소 삭제

- O(1) 소요

## Doubly Linked List

- 양방향으로 이어지는 연결 리스트
- Singly Linked List보다 자료구조의 크기가 조금 더 크다.

### 요소 찾기

- O(n) 소요

### 요소 추가

- O(1) 소요

### 요소 삭제

- O(1) 소요

## Circular Linked List

- Singly 혹은 Doubly Linked List에서 Tail이 Head로 연결되는 연결 리스트
- 메모리를 아껴쓸 수 있으며 원형 큐 등을 만들때도 사용된다.

## JavaScript(단일 연결리스트)

```jsx
class Node {
	constructor(value){
		this.value = value;
		thie.next = null;
	}
}

class SinglyLinkedList {
	constructor(){
		this.head = null;
		this.tail = null;
	}

	find(value){
		let currNode = this.head;
		while(currNode.value !== value){
			currNode = currNode.next;
		}
		return currNode;
	}

	append(newValue){
		const newNode = new Node(newValue);
		if(this.head === null){
			this.head = newNode;
			this.tail = newNode;
		}else{
			this.tail.next = newNode;
			this.tail = newNode;
		}
	}

	insert(node, newValue){
		const newNode = new Node(newValue);
		newNode.next = node.next;
		node.next = newNode;
	}

	remove(node, newValue){
		let prevNode = this.head;
		while(prevNode.next.value !== value){
			prevNode = prevNode.next;
		}
		if(prevNode.next !== null){
			prevNode.next = prevNode.next.next;
		}
	}
}
```