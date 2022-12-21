# Ch3(배열)

# 배열(순차 리스트)

## 배열이란?

- 연관된 데이터를 연속적인 형태로 구성된 구조를 가진다.
- 배열에 포함된 원소는 순서대로 번호(index)가 붙는다.

## 배열의 특징

- 고정된 크기를 가지며 일반적으론 동적으로 크기를 늘릴 수 없다.
    - 자바스크립트처럼 대부분의 스크립트 언어는 동적으로 크기가 증감되도록 만들어져 있다.
- 원하는 원소의 index를 알고 있다면 O(1)로 원소를 찾을 수 있다.
- 원소를 삭제하면 해당 index에 빈자리가 생긴다.

## 배열 요소 삭제

- 삭제 후 순서를 맞추려면 O(n)이 소요된다.

## 배열 요소 추가

- 중간에 요소를 추가하고 싶다면 O(n)이 소요된다.
- 따라서 추가와 삭제가 반복되는 로직이라면 배열 사용을 권장하지 않는다.

## JavaScript에서 사용법

### 배열생성

```jsx
// 빈 Array를 생성할 수 있다.
let arr1 = [];
console.log(arr1);

// 미리 초기화된 Array를 생성할 수 있다.
let arr2 = [1, 2, 3, 4, 5];
console.log(arr2);

// 많은 값을 같은 값으로 초기화할 경우 fill을 쓸 수 있다.
let arr3 = Array(10).fill(0);
console.log(arr3);

// 특정 로직을 사용하여 초기화할 경우 from을 사용할 수 있다.
let arr4 = Array.from({length : 100}, (_, i) => i);
console.log(arr4);
```

### 배열 요소 추가, 삭제

```jsx
const arr = [1, 2, 3];
console.log(arr);

// 끝에 추가
arr.push(4); // O(1)
arr.push(5, 6); // O(1)
console.log(arr); // [1,2,3,4,5,6]

// 3번 인덱스에 128을 추가
arr.splice(3, 0, 128); // O(n)
console.log(arr);

// 3번 인덱스 값을 제거한다.
arr.splice(3, 1); // O(n)
console.log(arr[3]); // 4
```

### 특이점

```jsx
// 자바스크립트의 Array는 다른 언어의 Array와 조금 다르다.
// 자바스크립트 Array는 동적이다.
const arr = [];
console.log(arr);
arr.push(1);
arr.push(1);
arr.push(2);
arr.push(3);
console.log(arr);

// 자바스크립트의 Array는 HashMap에 가깝다.
console.log(arr.length); // 4
// index가 number가 아니어도 된다.
arr["string"] = 10;
arr[false] = 0;
console.log(arr);
console.log(arr.length);
arr[4] = 5;
console.log(arr.length);
```

# 자바스크립트 배열과 객체

## 배열

- 연간된 데이터를 연속적인 형태로 저장하는 복합 타입
- 배열에 포함된 원소는 순서대로 번호(index)가 붙는다.
- 출석부에 비유할 수 있다.

## 객체

- 객체는 여러 값을 키-값 형태로 결합시킨 복합타입
- 사물함에 비유할 수 있다.

## JavaScript 실습(배열)

```jsx
const arr1 = new Array();
const arr2 = [];
const arr3 = [1,2,3,4,5];
const arr4 = new Array(5);
const arr5 = new Array(5).fill(5);
const arr6 = Array.from(Array(5), (v, i) => i+1)

console.log(arr1);
console.log(arr2);
console.log(arr3);
console.log(arr4);
console.log(arr5);
console.log(arr6);
```

```jsx
const arr = [1,2,3,4,5,6];

console.log(arr.length);
arr.length = 3;
console.log(arr);
arr.length = 10;
console.log(arr);
```

```jsx
const arr = [1, 2, 3, 4, 5, 6];

// join
console.log(arr.join(', '));

// reverse
// 주의해야할점 : 원래 배열에도 영향을 줌
console.log(arr.reverse());

const arr1 = [1,2,3,4,5,6];
const arr2 = [7,8,9,10];

// concat
console.log(arr1.concat(arr2));

```

```jsx
const arr = [1,2,3,4,5,6];

// push, pop
arr.push(7);
arr.push(8, 9, 10);
console.log(arr);
arr.pop();
arr.pop();
console.log(arr.pop());
console.log(arr);
```

```jsx
const arr = [1,2,3,4,5,6];

// shift, unshift
arr.shift();
arr.shift();
console.log(arr);
arr.unshift(10);
console.log(arr);
```

```jsx
const arr = [1,2,3,4,5,6];

// slice
console.log(arr.slice(2, 4));
console.log(arr); // 원본 배열은 변화 없음
```

```jsx
const arr = [1,2,3,4,5,6];

// splice
arr.splice(2,2);
```

```jsx
const arr = [1,2,3,4,5,6];

for(let i = 0; i < 5; i+=1){
	console.log(arr[i]);
}

// for of
for(const item of arr){
	console.log(item);
}
```

```jsx
const arr = [1,2,3,4,5,6];

console.log(typeof arr); // object

arr["key"] = "value"; // 추천 X
console.log(arr);
console.log(arr.length); // 배열의 길이는 변경되지 않는다.

```

## JavaScript 실습(객체)

```jsx
const obj1 = new Object();
const obj2 = {};
const obj3 = { name: "이재준", company: "Super Company"};

console.log(obj1);
console.log(obj2);
console.log(obj3);
```

```jsx
const obj = { name: "이재준", company: "Super Company"};

obj["email"] = "jaeme0406@gmail.com";
console.log(obj);

obj.phone = "01012345678";
console.log(obj);

delete obj.phone;
console.log(obj);

console.log("email" in obj); // true
console.log("phone" in obj); // false

console.log(Object.keys(obj));
console.log(Object.values(obj));

// for in
for(const key in obj){
	console.log(key, obj[key]);
}
```