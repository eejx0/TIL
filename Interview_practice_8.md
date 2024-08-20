## 클로저

### 정의

<aside>
💡 **함수와 함수가 선언된 어휘적 환경의 조합**

</aside>

→ 함수를 지칭하고 그 함수가 선언된 환경과의 관계

→ 자신이 선언될 당시의 환경을 기억하는 함수

→ 내부함수가 외부함수의 context에 접근할 수 있는 것

### 특징

- 외부함수 스코프에서 내부함수 스코프로 접근 불가능
- 내부함수에서는 외부함수 스코프에서 선언된 변수에 접근 가능
- 외부 함수 스코프가 내부함수에 의해 언제든지 참조될 수 있음
    - 클로저를 남발할 경우 퍼포먼스 저하 발생
- 함수가 호출되는 환경과 별개로 기존에 선언되어 있던 환경을 기준으로 변수 조회

### 장점

1. **전역 변수 사용의 최소화**
    - 전역 변수가 많으면 의도치 않게 어디서든 접근하는 상황 발생
    - 클로저를 이용해 이러한 실수나 예외적인 상황 방지 가능
2. **데이터 보존 기능**
    - 외부함수의 실행이 끝나도 외부함수 내 변수 사용 가능
    - 특정 데이터를 스코프 안에 가둔 채로 계속 사용할 수 있게하는 폐쇄성 가짐
3. **모듈화를 통한 코드 재사용에 편리**
    
    모듈화: 함수의 재사용성을 극대화하고 함수 하나를 독립적인 부품의 형태로 분리하는 것
    
    - 클로저 함수를 변수에 할당하면 각자 독립적으로 값 사용하고 보존 가능
4. **정보의 접근 제한 (캡슐화)**
    
    캡슐화: 클로저 모듈 패턴으로 객체에 담아 여러 함수를 리턴하도록 만들어 정보의 접근 제한
    

### 예시

```jsx
function outer() {
	let message = 'Hello';
	
	return function inner(name) {
		return message = message + name;
	}
}

let greeting = outer();

console.log(greeting('euijin'))
```

→ outer 함수는 종료됐지만 내부 변수인 message는 inner로 접근 가능

**→ inner함수가 클로저**

## ==, ===

**==**

> a == b일 때 a와 b의 값이 같은지 비교해 같으면 true, 다르면 false
> 

**===**

> a === b 일 때 값과 값의 타입이 모두 같은지를 비교해 같으면 true, 다르면 false
> 

## 이벤트 루프

### 구조

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/ed08f4e9-4934-479f-a55b-09ffbf96beb6/25954a6b-d856-4ae9-afcd-f50a61c06607/image.png)

- **Memory Heap**
    
    메모리 할당이 일어남
    
- **Call Stack**
    
    실행된 코드의 환경을 저장하는 자료구조로 함수 호출 시 이곳에 저장 (선입후출)
    
- **Web APIs**
    
    브라우저에서 제공하는 API
    
- **Callback Queue**
    
    비동기적으로 실행된 콜백함수를 저장하는 자료구조 (선입선출)
    
- **Event Loop**
    
    Call Stack과 Callback Queue의 상태를 체크해 Call Stack이 비면 Callback Queue의 첫번째 콜백을 꺼내 Call Stack에 추가
    

### 예시

```jsx
console.log(1);

setTimeout(
	function cb() {
		console.log(2);
	}
, 0);

console.log(3);
```

1. console.log(1)이 Call Stack에 추가되고 실행된 후 Call Stack에서 제거됌
2. setTimeOut(…)이 Call Stack에 추가됌
3. setTimeOut(…)가 실행된 후 브라우저가 제공하는 timer Web API 호출하고 Call Stack에서 제거됌
4. console.log(3)이 Call Stack에 추가되고 실행된 후 Call Stack에서 제거됌
5. setTimeOut(…)의 0ms 시간이 지난 뒤 Callback으로 전달한 cb함수가 Callback Queue에 추가됌
6. Event Loop는 Call Stack이 비어있는 것을 확인하고 Callback Queue 살펴보고 함수 cb를 발견한 후 Call Stack에 cb함수 추가
7. cb 함수가 실행되고 내부의 console.log(2)가 Call Stack에 추가됌
8. console.log(2)가 콘솔에 출력되고 Call Stack에서 제거되고 cb함수도 제거됌

## Object와 Map의 차이점

> **Object**는 **크기를 수동으로 추적**해야하지만 **Map**은 **크기를 쉽게 얻을 수** 있음
> 

→ Object엔 prototype이 있어 Map에 기본 키들이 있음

→ Map은 삽입된 순서대로 반복됌

## 화살표 함수와 일반 함수의 차이점

### 일반 함수

<aside>
💡 **function 키워드**를 가지고 정의하는 방식

</aside>

→ 함수 선언식과 함수 표현식으로 정의 가능

### 화살표 함수

<aside>
💡 function 키워드 대신 화살표 ⇒ 를 사용해 이 전보다 간결한 문법으로 작성 가능

</aside>

→ 일반 함수와의 차이는 문법의 간결함

### 차이점

> this
> 

**일반 함수의 this**

> 함수가 어디에 선언되었든 상관없이 this 값은 함수를 호출한 객체를 가리킴
> 

→ 함수가 선언된 위치가 아닌 호출되는 방법에 따라 this가 결정됌

**화살표 함수의 this**

> 함수를 선언할 때 this에 바인딩할 객체가 결정됌
> 

→ 일반 함수가 자신만의 this를 갖는 것과 달리 언제나 상위 스코프의 this를 가리킴

## 타이머 함수

### 정의

<aside>
💡 일정 시간이 지난 후 특정 코드 또는 함수가 실행될 수 있도록 해주는 함수
일정 시간마다 함수가 실행될 수 있도록 해주는 함수

</aside>

### 종류

- setTimeout(함수, 시간): 일정 시간 후 함수 실행
- setInterval(함수, 시간): 시간 간격마다 함수 실행
- clearTimeout(): 설정된 Timeout 함수 종료
- clearInterval(): 설정된 Interval 함수 종료
