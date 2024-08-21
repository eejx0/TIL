## 스코프

<aside>
💡 **변수에 접근할 수 있는 범위**

</aside>

→ **전역 스코프**: js 코드의 최상위 레벨에 해당하는 스코프로 함수 어디에서든 접근 가능

→ **지역 스코프**: 특정 함수에 해당하는 스코프로 해당 함수 자신과 하위 함수에서만 자원에 접근 가능

## 전역 변수의 문제점

- **암묵적 결합**
    - 모든 코드가 전역 변수를 참조하고 변경할 수 있는 암묵적 결합 허용
    - 변수의 유효 범위가 커지며 코드의 가독성 나빠짐
    - 의도치 않게 상태가 변경될 위험성
- **긴 생명 주기**
    - 메모리 리소스를 오랜 시간 소비
    - var는 변수의 중복 선언을 허용
        - 생명주기가 긴 전역 변수는 변수 이름이 중복될 수 있음
        - 변수 이름이 중복되면 의도치 않은 재할당이 이루어짐
- **스코프 체인 상에서 종점에 존재**
    - 변수 검색 시 가장 마지막에 검색됌
- **네임스페이스 오염**
    - js는 파일이 분리되어 있어도 하나의 전역 스코프 공유

## proto와 prototype의 차이

**proto**

- 모든 객체가 가지고 있음
- 하나의 Link라고 할 수 있음

**prototype**

- new로 인스턴스를 만들 때 proto를 생성하는데 사용
- 함수 객체만 갖고 있음
- 생상자를 가지는 원형으로 선언 가능

## this란?

### 정의

<aside>
💡 자바스크립트에서 this는 현재 실행 중인 코드에서 **자신이 속한 객체 또는 자신이 생성할 인스턴스를 가리키는 자기 참조 변수**

</aside>

> this는 함수 호출 방식에 의해 동적으로 결정됌
> 
- 일반 함수로 호출된 경우 this는 전역 객체 (이 this는 브라우저에서 window 객체가 됌)
- 메소드로 호출된 경우 this는 해당 메서드가 속한 객체를 가리킴
- 함수가 호출될 때 apply, call 또는 bind가 사용되었으면 첫번째 인자로 전달하는 값에 this 바인딩
- 함수가 호출될 때 생성자 함수 내부에서 this는 생성자 함수가 생성할 인스턴스가 바인딩

### 일반 함수의 this

```jsx
function traditionalFunction() {
	console.log(this);
}

const obj = { method: traditionalFunction };
obj.method(); // this가 obj를 참조
```

→ 일반 함수에서 this는 함수를 호출한 객체를 참조

→ 기본적으로 this엔 전역 객체가 바인딩 됌

### 화살표 함수의 this

```jsx
const obj = {
	method: function() {
		const arrowFunction = () => {
			console.log(this);
		};
		arrowFunction();
	}
};

obj.method(); // this가 obj를 참조
```

→ 화살표 함수는 this를 자신이 정의된 위치에서 상속받음

→ 화살표 함수 내부의 this는 화살표 함수가 정의된 위치의 this와 동일

### 화살표 함수 vs 일반 함수

```jsx
const obj = {
	name: 'Name',
	traditionalFunction: function() {
		console.log(this.name);
	},
	arrowFunction: () => {
		console.log(this.name);
	}
};

obj.traditionalFunction(); // 'Name' 출력
obj.arrowFunction(); // undefined 출력
```

→ traditionalFunction은 obj 내에서 호출되어서 this는 obj를 참조

→ arrowFunction은 obj내에서 정의되었지만 그 함수가 상위 스코프의 this를 상속받아 undefined

### ~ 에서 this는 무엇을 가리킬까

- 글로벌 컨텍스트
    - 브라우저 환경에선 window 객체
    - Node.js 환경에선 global 객체
- 일반 함수
    - 해당 함수를 호출한 객체
    - 엄격 모드에선 undefined
- 메서드: 메서드를 소유한 객체
- 생성자 함수: 새로 생성된 인스턴스 객체
- 이벤트 핸들러: 이벤트가 발생한 DOM 요소
- 화살표 함수: 화살표 함수가 정의된 위치의 상위 스코프의 this
