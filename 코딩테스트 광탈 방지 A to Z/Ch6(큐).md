# 큐

- First In First Out이라는 개념을 가진 선형 자료구조이다.
- Linear Queue와 Circular Queue가 존재한다.
- 대기열을 예시로 들 수 있다.

## Linear Queue

- Linear Queue는 Array로 표현이 가능하다.(조금 어려움)
- Linked List로 표현하자.

### JavaScript 사용법(Array) : 코딩테스트 추천

```jsx
class Queue {
	constructor() {
		this.queue = [];
		this.front = 0;
		this.rear = 0;
	}
	
	enqueue(value){
		this.queue[this.rear++] = value;
	}

	dequeue(){
		const value = this.queue[this.front];
		delete this.queue[this.front];
		this.front += 1;
		return value;
	}

	peek(){
		return this.queue[this.front];
	}

	size(){
		return this.rear - this.front;
	}
}
```

### JavaScript 사용법(LinkedList)

```jsx
class Node {
	constructor(value){
		this.value = value;
		this.next = null;
	}
}

class Queue {
	constructor(){
		this.head = null;
		this.tail = null;
		this.size = 0;
	}

	enqueue(newValue){
		const newNode = new Node(newValue);
		if(this.head === null){
			this.head = this.tail = newNode;
		}else {
			this.tail.next = newNode;
			this.tail = newNode;
		}
		this.size += 1;
	}

	dequeue(){
		const value = this.head.value;
		this.head = this.head.next;
		this.size -= 1;
		return value;
	}

	peek(){
		return this.head.value;
	}
}
```

### shift 함수는 쓰지말자

```jsx
const queue = [1, 2, 3];
queue.push(4);
const value = queue.shift(); // O(n) 
console.log(value);
```

## Circular Queue

- Front와 Rear가 이어져있는 Queue
- Circular Queue는 Linked List로 구현했을 때 이점이 없다.

### JavaScript 사용법(Array) : 코딩테스트에서 환형큐를 써야할 상황은 거의 없다.

```jsx
class Queue{
	constructor(maxSize){
		this.maxSize = maxSize;
		this.queue = [];
		this.front = 0;
		this.rear = 0;
		this.size = 0;
	}

	enqueue(value){
		if(this.isFull()){
			console.log("Queue is full.");
			return;
		}
		this.queue[this.rear] = value;
		this.rear = (this.rear + 1) % this.maxSize;
		this.size += 1;
	}

	dequeue(){
		const value = this.queue[this.front];
		delete this.queue[this.front];
		this.front = (this.front + 1) % this.maxSize;
		return value;
	}

	isFull(){
		return this.size === this.maxSize;
	}

	peek(){
		return this.queue[this.front];
	}
}
```

## 큐 프린터 실습(내코드)

```jsx
class Queue {
    constructor(){
        this.queue = [];
        this.front = 0;
        this.rear = 0;
    }
    enqueue(value){
        this.queue[this.rear++] = value;
    }
    dequeue(){
        const value = this.queue[this.front];
        delete this.queue[this.front];
        this.front++;
        return value;
    }
    peek(){
        return this.queue[this.front];
    }
}

function solution(priorities, location) {
    var answer = 0;
    const queue = new Queue();
    // priorities 중요도 배열
    // location : 현재 위치
    
    priorities.forEach((prioritie, i) => {
       queue.enqueue([prioritie, i])
    })
    
    // 내림차순 정렬
    priorities.sort((a,b) => b-a);

    let count = 0;
    while(true){
        let currentValue = queue.peek();
        if(currentValue[0] < priorities[count]){
            queue.enqueue(queue.dequeue());
        
        }else {
            const value = queue.dequeue();
            count += 1;
            if(location === value[1]){
                return count;
            }
        }
    }
    
    return count;
}
```

## 큐 프린터 실습(강사풀이)

```jsx
class Node {
	constructor(value){
		this.value = value;
		this.next = null;
	}
}

class Queue {
	constructor(){
		this.head = null;
		this.tail = null;
	}

	enqueue(newValue){
		const newNode = new Node(newValue);
		if(this.head === null){
			this.head = this.tail = newNode;
		}else {
			this.tail.next = newNode;
			this.tail = newNode;
		}
		this.size += 1;
	}

	dequeue(){
		const value = this.head.value;
		this.head = this.head.next;
		this.size -= 1;
		return value;
	}

	peek(){
		return this.head.value;
	}
}

function solution(priorities, location){
	const queue = new Queue();
	for(let i = 0; i < priorities.length; i += 1){
		queue.enqueue([priorities[i], i]);	
	}

	priorities.sort((a, b) => b - a);

	let count = 0;
	while(true){
		const currentValue = queue.peek();
		if(currentValue[0] < priorites[count]){
			queue.enqueue(queue.dequeue());
		} else {
			const value = queue.dequeue();
			count += 1;
			if(location === value[1]){
				return count;
			}
		}
	}

	return count;
}
```