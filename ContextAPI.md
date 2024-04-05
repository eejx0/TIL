# Context API

## 사용 이유 (Props의 불편한 점)

### Context ?

<aside>
💡 리액트 컴포넌트 간에 **어떤 값을 공유**할 수 있게 해주는 기능

</aside>

→ 주로 전역적으로 필요한 값을 다룰 때 사용

→ 리액트 컴포넌트에서 **Props가 아닌 다른 방식**으로 컴포넌트 간에 값을 전달하는 방법!

### Props로만 데이터를 전달하면 ?

> 깊숙히 위치한 컴포넌트에 데이터를 전달해야 하는 경우 여러 컴포넌트를 거쳐 연달아 Props를 설정해줘야 함 → 불편
> 

> 컴포넌트를 만들 때 여러 종류의 자식 컴포넌트가 특정 값에 의존을 한다면 각 컴포넌트에 다양한 Props가 들어있고 구조가 까다로웠다면 → 가독성 떨어짐
> 

* Props Drilling

Props를 컴포넌트 여러개 거쳐 전달하게되면 불편하게 되는 코드,,

## Context

### Context 사용법

리액트 패키지에서 createContext 함수를 불러와서 만듬

```jsx
import { createContext } from 'react';
const MyContext = createContext;
```

```jsx
function App() {
	return (
		<MyContext.Provider value="Hello World">
		  <GrandParent />
    </MyContext.Provider>
	)
}
```

→ Context 객체 안엔 Provider라는 컴포넌트가 들어있음

→ 컴포넌트 간 공유하고자 하는 값을 value라는 Props로 설정

자식 컴포넌트들에서 해당 값에 접근 가능

### Context에서 상태 관리는 ??

```jsx
import { createContext } from 'react';

const CounterContext = createContext();

function CounterProvider({ children }) {
  return <CounterContext.Provider>{children}</CounterContext.Provider>;
}

function App() {
  return (
    <CounterProvider>
      <div>
        <Value />
        <Buttons />
      </div>
    </CounterProvider>
  );
}
```

→ children Props를 받아와서 CounterContext.Provider 태그 사이에 넣기

→ 필요한 기능들 CounterProvider 컴포넌트 안에서 구현

```jsx
import { children, useState } from 'react';

const CounterContext = createContext();

function CounterProvider({ children }) {
	const counterState = useState(1);
	return (
		<CounterContext.Provider value={counterState}>
			{children}
		</CounterContext.Provider>
	)
}
```

→ 하나의 상태만 있는 경우 useState로 만들어자니 값, 함수가 들어있는 배열 통째로 value에 넣음

```jsx
import { createContext, useContext, useState } from 'react';

function useCounterState() {
	const value = useContext(CounterContext);
	return value;
}
```

→ Hook을 이렇게 준비하면 CounterProvider의 자식 컴포넌트 어디든지 useConterState 사용해 값 조회 or 변경 가능

### 마무리

> 상태관리 라이브러리와 Context는 완전히 별개의 개념이다!
> 

Context는 전역 상태 관리를 할 수 있는 수단일 뿐,,
상태관리 라이브러리는 상태관리를 더 편하고 효율적으로 할 수 있게 해주는 기능 제공
