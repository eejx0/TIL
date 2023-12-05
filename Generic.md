# Generics

> TypeScript
> 

<aside>
💡 타입을 함수의 매개변수처럼 사용하는 것

</aside>

**기본 문법**

```tsx
function getText<T>(text: T): T {
	return text;
}
```

```tsx
getText<string>('hi');
getText<number>(10);
getText<boolean>(true);
```

**사용 이유**

```tsx
function logText(text: any): any {
	return text;
}
```

> 함수의 입력 값에 대한 타입과 출력 값에 대한 타입이 동일한지 검증 😉
> 

### 제네릭 타입 변수

```tsx
function logText<T>(text: T): T {
	console.log(text.length); // Error: I doesn't have .length
	return text;
}
```

**why**❓ 👉🏻 text에 .length가 있다는 단서가 없음

```tsx
function logText<T>(text: T[]): T[] {
	console.log(text.length);
	return text;
}
```

```tsx
function logText<T>(text: Array<T>): Array<T> {
	console.log(text.length);
	return text;
}
```
