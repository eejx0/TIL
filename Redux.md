# Redux

<aside>
💡 **Redux**란 React와 React Native에서 가장 많이 사용되고 있는 **상태 관리 라이브러리**

</aside>

→ React의 전역에서 각 화면에서 필요한 상태값을 분리시켜 관리

→ 다른 페이지를 이동하는 과정에서 데이터 손실이 일어날 가능성 x

→ 효율적으로 데이터 관리 가능!

Context API를 사용하면❔

프로젝트의 규모가 커지게 되어 많은 상태값을 선언해야할 경우 Redux를 사용해야 함

### 액션 (Action)

> **상태에 어떤 변화**가 필요할 때 액션이 발생
액션은 객체 형식으로 선언되어야함!
> 

```tsx
{
	type: 'ACTION_TYPE',
	data: { ... }
}
```

→ type 필드는 액션 객체의 이름과 같은 역할을 하게 됌

무조건 type이라는 명칭의 필드가 선언되어야 함

→ data는 액션을 통해 상태가 변화해야할 때 참고해야할 데이터가 됌

꼭 필드의 이름이 data가 될 필요는 없음

### 액션 생성 함수 (Action Creator)

> **액션 객체**를 **생성**
매번 변화가 있을때마다 액션 객체를 작성하는 것에 대한 불편함 &
데이터 누락 문제 방지 → **함수로 묶어 관리**
> 

```tsx
const creator = (value) => {
	return {type: 'ACTION_TYPE', payload: value}
}
```

### 리듀서 (Reducer)

> 액션 객체를 통해 받은 **데이터로 변화**를 일으킴
> 

```tsx
const initialState = {
	count: 0
}

function reducer(state=initialState, action) {
	switch(action.type) {
		case INCREMENT:
			return {
				...state,
				count: state.count+1
			};
		case DECREMENT:
			return {
				...state,
				count: state.count-1
			}
	}
}
```

### 스토어 (Store)

> 프로젝트에 **Redux를 적용**하기 위해 생성해야 하는 것
Redux를 설계할 땐 단일 store가 원칙 → 한 개의 프로젝트는 단 하나의 Store만 가질 수 있음
> 

### 디스패치 (Dispatch)

> Store의 내장 함수 → **액션을 발생**시키는 것
함수가 호출되면 Store는 **Reducer함수를 실행**시켜 **새로운 상태**를 만듬
>
