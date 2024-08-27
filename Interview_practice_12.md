## TypeScript
### 장점

> **JS 슈퍼셋**
> 

→ 기존 JS와 완벽하게 호환함 (다른 언어가 아니기 때문)

→ Migration하기도 편하고 ts와 js를 혼합해 사용하기에도 무리가 없음

> **컴파일 언어이자 정적 타입 언어**
> 

→ 개발 단계에서 오류를 잡을 수 있고 개발 단계에서의 안정성을 높여줄 수 있음

→ 타입을 미리 체크해 실행시간이 JS에 비해 빠름

> **객체 지향**
> 

→ JS가 불가능하다는 것은 아니지만 TS가 더 편함

→ prototype, class, object 등을 이용해 JS도 가능하지만 interface, type이 없는 JS 보단 TS가 쉽게 설계가 가능함

### 단점

> 러닝 커브
> 

→ 배우는 데에 있어 많은 어려움을 겪음

→ ex) any 남발, 쓸데없이 코드 수 늘리기

> 코드 수
> 

→ 라인이 늘어나 가독성이 더 안좋다고 보는 사람이 많음

## JS와 TS

### 차이점

TypeScript는 JavaScript 기반의 언어

**JavaScript**

- 클라이언트 측 스크립팅 언어
    - 사용자가 브라우저를 열고 페이지를 요청하면 해당 요청이 웹 서버로 이동
- 이벤트 생성 수행
- 멀티 스레딩, 멀티 프로세싱 기능 x

**Typescript**

- 객체 지향 컴파일 언어
- JavaScript의 상위 집합
    - JavaScript의 모든 기능 O
- TS 컴파일러로 ts파일을 js파일로 변환
- 정적 유형 검사 제공
- 클래스 기반 객체 만들 수 있음
- 클래스 기반이라 객체 지향 프로그래밍 언어로 상속, 캡슐화, 생성자 지원

### 사용하며 느낀 점

## TS에서 type과 interface 차이

### 상속하는 법

**interface**

extends 키워드로 확장가능

```tsx
interface Person {
	name: string;
}

interface Student extends Person {
	school: string;
}

const euijin: Student = {
	name: "euijin",
	school: 'DSM'
}
```

**type**

&로 확장 가능

```tsx
type Person = {
	name: string
}

type Student = Person & {
	school: string
}

const euijin: Student = {
	name: "euijin",
	school: "DSM"
}
```

### 선언적 확장

**interface**

선언적 확장 가능
→ 같은 이름의 interface 선언하면 자동으로 확장됨

```tsx
interface Person {
	name: string;
}

interface Person {
	gender: string;
} // 선언적 확장

const euijin: Person = {
	name: 'euijin',
	gender: 'female'
}
```

**type**

선언적 확장 불가능
→ 타입 객체의 확장성을 위해선 interface를 사용하는 것이 더 좋음

```tsx
type Person = {
	name: string;
}

type Person = { 
	gender: string;
} // Error: Duplicate identifier 'Person'
```

### 자료형

**interface**

- **객체의 타입을 설정할 때 사용 가능**
- **원시 자료형엔 사용 불가능**

```tsx
interface Person {
	name: string;
	gender: string;
} // 가능
```

```tsx
interface name extends string { } // 불가능
```

**type**

- 객체의 타입을 설정할 때 사용 가능
    - 이땐 interface를 사용하는게 좋음
- 원시값이나 튜플, 유니언 타입 선언할 때 type 사용하는 것이 좋음

```tsx
type Name = string; // primitive
type Person = [string, number, boolean]; // tuple
type NumberString = string | number; // union
```

```tsx
type Person = { // 인터페이스를 사용하자
	name: string,
	gender: string
}
```

### computed value 사용

**interface**

- 불가능

```tsx
type Subjects = 'math' | 'science';

interface Grades {
	[key in Subjects]: string;
} // error: a mapped type may not declare properties or methods
```

**type**

- 가능

```tsx
type Subjects = 'math' | 'science';

type Grades = {
	[key in Subjects]: string;
}
```

> **type**은 **모든 타입을 선언**할 때 사용할 수 있고
**interface**는 **객체에 대한 타입을 선언**할 때만 사용할 수 있음

**확장 불가능**한 타입을 선언하고 싶다면 **type** 사용
**확장 가능**한 타입을 선언하고 싶다면 **interface** 사용
> 

## Typescript의 데코레이터

### 정의

<aside>
💡 일종의 **함수로 코드 조각을 장식**해주는 역할
타입스크립트에서는 그 기능을 **함수로 구현**하는 것

</aside>

→ 타입스크립트에서 실험적으로 도입된 기능

→ 자바의 어노테이션, 파이썬의 데코레이터와 유사한 기능 (파이썬의 데코레이터와 더 유사)

### 특징

- 클래스 선언, 메서드, 접근자, 프로퍼티, 매개변수에 첨부할 수 있는 특수한 종류의 선언
- 데코레이터 함수에는 target, key, descriptor가 전달됨
- 메소드나 클래스 인스턴스가 만들어지는 런타임에 실행됨
    - 매번 실행되지 않음
- 클래스 또는 클래스 내부 생성자, 프로퍼티, 접근자, 메서드, 매개변수에만 장식될 수 있음

## 언제 any 타입 사용하는지

1. **마이그레이션** 중일 때
    
    JS 코드베이스를 TS로 변환할 때 모든 코드에 대해 정확한 타입을 정의하기 어려울 수 있어 이런 경우 any를 사용해 오류를 피하고 나중에 구체적인 타입 추가
    
2. **복잡하거나 불명확한 타입**을 다룰 때
3. **타입 정의가 없는 외부 라이브러리**를 사용할 때
