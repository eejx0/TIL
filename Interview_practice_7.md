## lodash

### lodash?

<aside>
💡 **Javascript의 라이브러리**

</aside>

> 보통 array, collection 등 데이터의 필수적인 구조를 쉽게 다룰 수 있게하는데 사용됨
> 
- JS에서 배열 안의 객체들의 값을 handling할 때 유용함
- JS의 코드를 줄여주고 빠른 작업에 도움이 됨
- 브라우저에서 지원하지 않는 성능이 보장되어있는 다양한 메소드 가짐
- 퍼포먼스 측면에서 native보다 더 나은 성능
- npm이나 다른 패키지 매니저를 통해 쉽게 사용 가능

### lodash method

**array 관련 method**

- findIndex(): 배열 내에서 원하는 index 쉽게 구할 수 있음
- flatten(): 다차원 배열 내의 요소를 출력하는데 편리
- remove(): 배열 내의 조건에 맞는 요소들을 제거한 후 반환

**collection 관련 method**

- every(): 배열 안 요소들의 값들을 비교하고 분석하는데 용이
- find(): 조건을 만족하는 컬렉션에서의 첫번째 요소를 찾음
- filter(): 특정 조건을 만족하는 모든 요소를 추출하는 메소드
- map(): 계산 결과 배열 함수 실행, 그 결과를 배열로 반환
- forEach(): 배열의 값마다 함수 실행시킬 때 용이
- includes(): collection에 target 값이 있는지 판별
- reduce(): 첫번째 인자에 대해 배열 내부의 값을 통해 콜백함수 실행 후 결과값 반환

## JavaScript event delegation

이벤트 위임

<aside>
💡 비슷한 방식으로 여러 요소를 다뤄야할 때 사용

</aside>

→ 이벤트 캡쳐링과 이벤트 버블링을 활용하면 강력한 이벤트 핸들링 패턴인 이벤트 위임 구현 가능

→ 요소마다 핸들러를 할당하지 않고 공통 조상에 하나만 할당해도 여러 요소 한꺼번해 다룰 수 있음

→ 공통 조상에 할당한 핸들러에서 `event.target` 이용 시 어디서 이벤트가 발생했는지 알 수 있음

## Debounce의 역할

> 유저가 입력할 때마다 코드를 한 번씩만 실행되도록 해주는 함수
> 

ex) 검색 API에서 ‘안녕하세요’를 검색창에 친다고 하면 각 글자를 입력할 때마다 API를 요청하게됌 
→ 서버 자원의 부담

1. window 객체에 사용자가 입력할 때마다 발생하는 input 이벤트 등록
2. debounce 함수를 호출해 input 이벤트가 발생할 때마다 실행되는 함수 전달
3. debounce 함수는 내부적으로 타이머를 실행해 일정 시간이 지난 후에 함수 실행

## 이벤트 버블링과 캡처링

### 이벤트 버블링

> 특정 엘리먼트에 이벤트가 발생하면 해당 이벤트가 엘리먼트의 조상들에게까지 전달되는 현상
> 

```html
<body>
	<div class="one">
		<div class="two">
			<div class="three">
			</div>
		</div>
	</div>
</body>
```

```jsx
const divWrapper = document.querySelectorAll('div');
divWrapper.forEach(function(div){
	div.addEventListener('click', console);
})

function console(e) {
	console.log(e.currentTarget.className);
}
```

- 실행 결과
    
    three
    
    two
    
    one
    

→ 브라우저는 특정 화면 요소에 이벤트 발생 시 그 이벤트를 최상위에 있는 화면 요소까지 전파시킴

→ 이와 같이 하위에서 상위 요소로 이벤트를 전파하는 방식을 이벤트 버블링이라고 함

### 이벤트 캡쳐링

> 특정 엘리먼트에 이벤트가 발생하면 이벤트가 최상단의 부모 엘리먼트로부터 
전달되어져 내려오는 현상
> 
- 전달되는 이벤트는 부모 엘리먼트의 이벤트 핸들러를 작동시킴
- 캡쳐링 수행을 위해 이벤트 핸들러에 {capture: true} 또는 true로 캡쳐링 옵션을 true로 해줘야함
- 디폴트는 false라 다른 옵션을 설정하지 않으면 캡쳐링 일어나지 않음

```html
<body>
	<div class="one">
		<div class="two">
			<div class="three">
			</div>
		</div>
	</div>
</body>
```

```jsx
var divWrapper = document.querySelectorAll('div');
divWrapper.forEach(function(div) {
	div.addEventListener('click', console, {
		capture: true
	})
})

function console(e) {
	console.log(e.currentTarget.className);
}
```

- 실행 결과
    
    one
    
    two
    
    three
