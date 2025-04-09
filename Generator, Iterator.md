# Generator, Iterator
### iterator

> **반복을 위해 설계된 특정 인터페이스가 있는 객체**
> 

→ `{value, done}` 반환, `next` 메서드 가짐

이터러블하다: 자바스크립트에서 반복되는 열거 가능한 속성이 있는 객체
이터러블한 객체: string, array, map, set …

<aside>
🤔

**이터레이터가 배열과 다른 점은**

---

배열은 전체 값이 할당되어야 하지만 이터레이터는 무한대로 표현 가능

</aside>

```tsx
const alphabet = ['a', 'b', 'c', 'd'];
const it = alphabet.values();

it.next(); // {value: 'a', done: false}
it.next(); // {value: 'b', done: false}
it.next(); // {value: 'c', done: false}
it.next(); // {value: 'd', done: false}
it.next(); // {value: undefined, done: true}
it.next(); // {value: undefined, done: true} 
```

- next() 메소드를 반복적으로 호출해 명시적으로 반복시킬 수 있음
- value가 다음 시퀀스 값을 반환하고 done은 시퀀스의 마지막 값이 산출되었는지 여부를 반환

### generator

> **이터레이터 객체를 반환하는 함수**
> 

<aside>
🤔

**제너레이터가 일반함수와 다른 점은**

---

- 함수의 실행을 제어할 수 있음
- 실행된 yield 문이 제너레이터의 마지막 시퀀스라도 함수가 끝나는게 아니라 계속 next() 호출 가능
</aside>

```tsx
function *CreateIterator() {
	yield 1;
	yield 2;
	yield 3;
}

let iterator = CreateIterator();
console.log(iterator.next().value); // 1
console.log(iterator.next().value); // 2
console.log(iterator.next().value); // 3
```

- 함수 이름 앞에 붙은 *는 이 함수가 제너레이터 함수라는 의미
- yield: next()가 호출될 때 이터레이터가 리턴할 결과 값을 리턴될 순서대로 지정
- 모든 값을 리턴하지 않고 첫번째 시퀀스를 돈 후 다음 next()가 호출될 때까지 실행을 멈춤
