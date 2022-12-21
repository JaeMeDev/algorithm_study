# Ch2(자료구조의 종류와 시간복잡도)

# 자료구조의 종류

## 자료구조란

- 메모리를 효율적으로 사용하며 빠르고 안정적으로 데이터를 처리하는 것이 궁극적인 목표로 상황에 따라 유용하게 사용될 수 있도록 특정 구조를 이루고 있다.
- 일차원인 컴퓨터 메모리를 현실에 대응되도록 구조를 만든 것이라 할 수 있다.

## 선형 구조

- 한 원소 뒤에 하나의 원소 만이 존재하는 형태로 자료들이 선형으로 나열되어 있는 구조를 가진다.
- 선형 구조에 해당되는 자료구조는 배열, 연결리스트, 스택, 큐 등이 있다.

## 비선형 구조

- 원소 간 다대다 관계를 가지는 구조로 계층적 구조나 망형 구조를 표현하기에 적절하다.
- 비선형 구조에 해당되는 자료구조는 트리와 그래프 등이 있다.

## 완벽한 자료구조는 없다

- 더 좋고 더 나쁜 자료구조는 없다.
- 특정 상황에서 유용한 자료구조와 덜 유용한 자료구조가 존재할 뿐이다.
- 우리는 상황에 맞게 적절한 자료구조를 선택하면 된다.

# 시간복잡도

## 빅오표기법

- O(1) < O(log n) < O(n) < O(n log n) < O(n²) < O(2ⁿ) < O(n!)
- 점근적 표현법을 따른다.

### O(n)

```jsx
for (let i = 0; i < n; i += 1){
	// ...
}
```

### O(log n)

```jsx
for(let i = 1; i < n; i *= 2){
	// ...
}
```

### O(n log n)

```jsx
for(let i = 0; i < n; i += 1){
	for(let j = 1; j < n; j *= 2){
		// ...
	}
}
```

### O(n²)

```jsx
for(let i = 0; i < n; i += 1){
	for(let j = 0; j < n; j += 1){
		// ...
	}
}
```

### 계수 법칙

- 상수 k가 0보다 클 때 f(n) = O(g(n))이면 kf(n) = O(g(n)이다.
- n이 무한에 가까울 수록 k의 크기는 의미가 없다.

```jsx
// 두 루프는 같은 O(n)으로 표기된다.
for(let i = 0; i < n; i += 1){
	// ...
}

for(let i = 0; i < n * 5; i += 1){
	// ...
}
```

### 합의 법칙

- f(n) = O(h(n))이고 g(n) = O(p(n))이면 f(n) + g(n) = O(h(n)) + O(p(n))이다.
- 빅오는 더해질 수 있다.

```jsx
// 두 루프를 합쳐 O(n + m)으로 표기할 수 있다.
// 계수 법칙에 의해 5는 사라진다.
for(let i = 0; i < n; i += 1){
	// ...
}

for(let i = 0; i < n * 5; i += 1){
	// ...
}
```

### 곱의 법칙

- f(n) = O(h(n))이고 g(n) = O(p(n))이면 f(n) * g(n) = O(h(n)) * O(p(n))이다.
- 빅오는 곱해질 수 있다.

```jsx
// 두 루프를 곱해 O(n^2)로 표기할 수 있다.
// 계수 법칙에 의해 5는 사라진다.
for(let i = 0; i < n; i += 1){
	for(let j = 0; j < n * 5; j += 1){
		// ...
	}
}
```

### 다항 법칙

- f(n)이 k차 다항식이면 f(n)은 O(nᵏ)이다.

```jsx
// 다음 루프는 O(n^3)로 표기할 수 있다.
for(let i = 0; i < n * n * n; i += 1){
	// ...
}
```

### 2가지만 기억하면 된다.

1. 상수항은 무시
2. 가장 큰 항 외엔 무시

## 성능 측정 방법

### Date 객체를 이용

```jsx
const start = new Date().getTime();

// ...

const end = new Date().getTime();
console.log(end - start);
```

# 자바스크립트의 9가지 코드 트릭

## 1. 구조 분해 할당을 이용한 변수 swap

→ ES6의 구조 분해 할당 문법을 사용하여 두 변수를 swap 할 수 있다.

```jsx
let a = 5, b = 10;
[a,b] = [b,a];
console.log(a,b); // 10 5
```

## 2. 배열 생성으로 루프 제거하기

→ 보통 단순히 범위 루프를 돌고 싶다면 다음과 같은 코드를 작성한다.

```jsx
let sum = 0;
for(let i = 5; i < 10; i += 1){
	sum += i;
}
```

→ 만약 범위 루프를 함수형 프로그래밍 방식으로 사용하고 싶다면 배열을 생성해서 사용할 수 있다.

```jsx
const sum = Array
	.from(new Array(5), (_, k) => k+5)
	.reduce((acc, cur) => acc + cur, 0);
```

## 3. 배열 내은 요소 제거하기

→ `Set` 을 이용할 수 있다.

```jsx
const names = ['Lee', 'Kim', 'Park', 'Lee', 'Kim'];
const uniqueNamesWithArrayFrom = Array.from(new Set(names));
const uniqueNamesWithSpread = [...new Set(names)]
```

## 4. Spread 연산자를 이용한 객체 병합

→ 두 객체를 별도 변수에 합쳐줄 수 있다.

```jsx
const person = {
	name: "Lee Jae-Jun",
	familyName: "Lee",
	givenName: "Jae-Jun"
};

const company = {
	name: "Super Company",
	address: "Seoul"
};

const leeJaeJun = {...person, ...company};
console.log(leeJaeJun);
```

## 5. &&와 ||활용

→ &&와 ||는 조건문 외에서도 활용될 수 있다.

```jsx
// ||
// 기본값을 넣어주고 싶을 때 사용할 수 있다.
// participantName이 0, undefined, 빈 문자열, null일 경우 'Guest'로 할당된다.
const name = participanName || 'Guest';

// &&
// flag가 true일 경우에만 실행된다.
flag && func();

// 객체 병합에도 이용할 수 있다.
const makeCompany = (showAddress) => {
	return {
		name: "Super Company",
		...showAddress && { address: "Seoul" }
	}
}

console.log(makeCompany(false));
console.log(makeCompany(true));
```

## 6. 구조 분해 할당 사용하기

→ 객체에서 필요한 것만 꺼내 쓰는 것이 좋다.

```jsx
const person = {
	name: "Lee Jae-Jun",
	familyName: "Lee",
	givenName: "Jae-Jun",
	company: "Super Company",
	address: "Seoul"
}

const { familyName, givenName } = person;
```

→ 객체를 생성할 때 프로퍼티 키를 변수 이름으로 생략할 수 있다.

```jsx
const name = "Lee Jae-Jun";
const company = "Super Company";
const person = {
	name,
	company
}
console.log(person);
```

## 7. 비구조화 할당 사용하기

→ 함수에 객체를 넘길 경우 필요한 것만 꺼내 쓸 수 있다.

```jsx
const makeCompany = ({name, address, serviceName}) => {
	return {
		name,
		address,
		serviceName
	}
};
const cobalt = makeCompany({name:"Super Company", address: "Seoul", serviceName: "Present"});
```

## 8. 동적 속성 이름

→ ES6에 추가된 기능으로 객체의 키를 동적으로 생성할 수 있다.

```jsx
const nameKey = "name";
const emailKey = "email";
const person = {
	[nameKey] : "Lee Jae-Jun",
	[emailKey] : "jaeme0406@gmail.com"
};
console.log(person);
```

## 9. !! 연산자를 사용하여 Boolean 값으로 바꾸기

→ !! 연산자를 이용하여 `0, null, 빈 문자열, undefined, NaN` 을 `false` 로 그 외에는 `true` 로 변경할 수 있다.