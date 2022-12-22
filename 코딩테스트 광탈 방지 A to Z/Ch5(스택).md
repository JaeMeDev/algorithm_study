# Ch5(스택)

# 스택

- Last In First Out이라는 개념을 가진 선형 자료구조다.
- 바닥이 막힌 상자를 생각하면 편하다.
- 프링글스 통을 생각하면 편하다.
- 스택 메모리를 생각하자.
- Stack을 Array로 표현할 수 있다.
- Stack을 LinkedList로 표현할 수 있다.

## Array로 Stack 구현(추천)

```jsx
const stack = [];

// Push
stack.push(1);
stack.push(2);
stack.push(3);
console.log(stack); // [1, 2, 3]

// Pop
stack.pop();
console.log(stack); // [1, 2]

// Get Top
console.log(stack[stack.length - 1]); // 2
```

## LinkedList로 구현

```jsx
class Node {
	constructor(value){
		this.value = value;
		this.next = null;
	}
}

class Stack {
	constructor(){
		this.top = null;
		this.size = 0;
	}

	push(value){
		const node = new Node(value);
		node.next = this.top;
		this.top = node;
		this.size += 1;
	}

	pop(){
		const value = this.top.value;
		this.top = this.top.next;
		this.size -= 1;
		return value;
	}

	size(){
		return this.size;
	}
}
```

## Stack 문제 풀기(올바른 괄호) - 나의 풀이

```jsx
function solution(s){
    // 처음이 여는 괄호가 아니거나 마지막이 닫는 괄호가 아닐때
    if(s.charAt(0) !== "(" || s.charAt(s.length -1) !== ")" ){
        return false;
    }
    
    const leftLength = [...s].filter((str) => str === "(").length;
    const rightLength = [...s].filter((str) => str === ")").length;
    
    // 여는 괄호의 수와 닫는 괄호의 수가 다를때
    if(leftLength !== rightLength){
        return false;
    }
    
    let count = 0;
    for(str of s){
        if(str === "("){
            count++;
            continue;
        }
        count--;
        if(count < 0) return false;
    }
    
    return true;
}
```

## Stack 문제 풀기(올바른 괄호) - 다른사람 풀이

```jsx
function solution(s){
    let answer = true;
    const stack = [];
    
    [...s].forEach((str) => {
        if(str === "("){
            stack.push("(")
            return;
        }
        if(stack.length === 0){
            answer = false;
            return;
        }
        stack.pop();
    })
    
    return answer && stack.length === 0;
}
```

## Stack 문제 풀기(올바른 괄호) - 강사 풀이1

```jsx
function solution(s){
	const stack = [];
	
	for(const c of s){
		if(c === "("){
			stack.push(c);
		}else {
			if(stack.length === 0){
				return false;
			}
			stack.pop();
		}
	}

	return stack.length === 0;
}
```

## Stack 문제 풀기(올바른 괄호) - 강사 풀이2

```jsx
function solution(s){
	let count = 0;

	for(const c of s){
		if(c === "("){
			count++;
		}else{
			if(count === 0){
				return false;
			}
			count--;
		}
	}

	return count === 0;
}
```