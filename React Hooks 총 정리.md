# React Hooks 총 정리

## useState

> 함수형 컴포넌트에서도 가변적인 상태를 지니고 있을 수 있게 해줌
> 

```jsx
const [value, setValue] = useState(0);
```

→ 기본 값을 0으로 설정

→ 배열의 첫번째 원소는 상태 값, 두번째 원소는 상태를 설정하는 함수

→ 하나의 useState함수는 하나의 상태 값만 관리 할 수 있음

## useEffect

> 리액트 컴포넌트가 렌더링 될 때마다 특정 작업을 수행하도록 설정
> 

**기본 구조**

```jsx
const [name, setName] = useState('');
const [nickname, setNickname] = useState('');

useEffect(() => {
	console.log('렌더링이 완료되었습니다');
	console.log({
		name,
		nickname
	});
});
```

→ 콘솔창을 보면 렌더링이 완료되었다고 뜨고 name, nickname 띄워짐

**마운트 될 때만 실행**

```jsx
useEffect(() => {
	console.log('마운트 될 때만 실행됩니다');
}, []); 
```

→ 컴포넌트가 화면에 가장 처음 렌더링 될 때만 실행됨

→ 업데이트 할 경우엔 실행할 필요가 없는 경우엔 함수의 두번째 파라미터로 빈 배열 넣기

**값이 업데이트 될 때만 실행**

```jsx
useEffect(() => {
	console.log(name);
}, [name]);
```

→ 두번째 파라미터로 전달되는 배열 안에 검사하고 싶은 값 넣기

→ 배열 안엔 useState로 관리하고 있는 상태나 props로 전달받은 값 넣기

→ 콘솔 창에 이름이 바뀔 때마다 이름이 띄워짐

## useContext

> 함수형 컴포넌트에서 Context를 더 쉽게 사용할 수 있음
> 

```jsx
import React, { createContext, useContext } from 'react';

const ThemeContext = createContext('black');
const ContextSample = () => {
	const theme = useContext(ThemeContext);
	const style = {
		width: '24px',
		height: '24px',
		background: theme
	}
}
```

→ 사용자 정보, 테마, 언어 등 전역적인 데이터를 전달하기에 편리

→ 상위 컴포넌트의 data가 필요한 하위 컴포넌트들은 useContext 훅을 사용해 해당 데이터를 받아오면 됌

## useReducer

> useState보다 컴포넌트에서 더 다양한 상황에 따라 다양한 상태를 다른 값으로 업데이트해주고 싶을 때 사용
> 

**리듀서**❔

현재 상태, 업데이트에 필요한 정보를 담은 액션값을 전달 받은 후 새로운 상태를 반환하는 함수

```jsx
function reducer(state, action) {
	return { ... }; // 불변성을 지키며 업데이트한 새로운 상태 반환
}
```

→ 액션값 ❔

```jsx
{
	type: 'INCREMENT',
}
```

**활용 코드**

```jsx
import React, { useReducer } from 'react';

function reducer(state, action) {
	switch (aciton.type) {
		case 'INCREMENT' :
			return { value: state.value + 1 };
		case 'DECREMENT' :
			return { value: state.value - 1 };
		default :
			return state;
			// 아무것도 해당되지 않을 때 기존 상태 반환
	}
}
const Counter = () => {
	const [state, dispatch] = useReducer(reducer, {value: 0})
	// 나중에 어떻게 사용하냐면..
	return (
		<div>현재 카운터 값은 <b>{state.value}</b>입니다. </div>
		<button onClick={() => dispatch({ type: 'INCREMENT' })}>+1</button>
		<button onClick={() => dispatch({ type: 'DECREMENT' })}>-1</button>
	)	
}
```

→ 첫번째 파라미터는 리듀서 함수

→ 두번째 파라미터는 해당 리듀서의 기본값

→ 함수 안에 파라미터로 액션 값 넣어주면 리듀서 함수가 호출되는 구조

## useMemo

> 리액트에서 컴포넌트의 성능을 최적화하는데 사용
> 

**memo**❔

momoization을 뜻하는데 해석하면 메모리에 넣기라는 의미

컴퓨터 프로그램이 동일한 계산을 반복해야 할 때 이전에 계산한 값을 메모리에 저장함으로써 동일한 계산의 반복 수행을 제거해 프로그램 실행 속도를 빠르게하는 기술

**기본 구조**

```jsx
const value = useMemo(() => {
	return calculate();
}, [item])
```

→ useEffect처럼 첫번째 인자로 콜백 함수, 두번째 인자로 의존성 배열을 받음

→ 의존성 배열 안에 있는 값이 업데이트 될때만 콜백 함수를 다시 호출해 저장된 값 업데이트

**활용 코드**

```jsx
import React, { useState, useMemo } from 'react';

const SimpleComponent = () => {
	const [numbers, setNumbers] = useState([1, 2, 3, 4, 5]);
	
	// numbers 배열의 합을 계산하는 함수를 최적화함
	const sum = useMemo(() => {
		console.log('합 구하는 중');
		return numbers.reduce((acc, cur) => acc + cur, 0);
	}, [numbers]);
	
	const addRandomNumber = () => {
    const randomNumber = Math.floor(Math.random() * 10) + 1;
    setNumbers([...numbers, randomNumber]);
  };
  
  return (
    <div>
      <h2>숫자들의 합: {sum}</h2>
      <button onClick={addRandomNumber}>랜덤 숫자 추가</button>
    </div>
  );
}
```

→ numbers 배열이 변경될 때만 sum을 다시 계산

→ 그렇지 않으면 기존에 계산된 값을 재사용해 불필요한 계산을 피해 성능 향상

## useCallback

> useMemo와 비슷한 함수로 주로 렌더링 성능을 최적화해야하는 상황에서 사용
이벤트 핸들러 함수를 필요할 때만 생성할 수 있음
> 

**useMemo와의 차이점**❔

useMemo는 자주 쓰이는 값을 캐싱해주고 그 값이 필요할 때 다시 계산을 하는 것이 아닌 useMemo를 통해 캐싱한 값을 메모리에서 꺼내와 재사용

useCallback도 같지만 useCallback은 인자로 전달한 콜백 함수 그 자체를 메모이제이션함

결국 useCallback은 함수를 useMemo는 값(또는 객체)를 최적화하는데 사용됌

**기본 구조**

```jsx
useCallback(() => {
	return value;
}, [item]);
```

**활용 코드**

```jsx
import React, { useState, useMemo, useCallback } from 'react';

const SimpleComponent = () => {
	const [numbers, setNumbers] = useState([1, 2, 3, 4, 5]);
	
	// useMemo를 사용해 numbers 배열의 합을 계산하는 함수를 최적화
	const sum = useMemo(() => {
		console.log('합 구하는 중');
		return numbers.reduce((acc, cur) => acc + cur, 0);
	}, [numbers]);
	
	// useCallback을 사용해 addRandomNumber 함수 최적화
	const addRandomNumber = useCallback(() => {
    const randomNumber = Math.floor(Math.random() * 10) + 1;
    setNumbers([...numbers, randomNumber]);
  }, [numbers]);
  
  return (
    <div>
      <h2>숫자들의 합: {sum}</h2>
      <button onClick={addRandomNumber}>랜덤 숫자 추가</button>
    </div>
  );
}
```

## useRef

> 함수형 컴포넌트에서 ref를 쉽게 사용할 수 있게 해줌
> 

```jsx
import React, { useState, useMemo, useCallback, useRef } from 'react';

const SimpleComponent = () => {
	const [numbers, setNumbers] = useState([1, 2, 3, 4, 5]);
	const prevNumberRef = useRef([]);
	
	// useMemo를 사용해 numbers 배열의 합을 계산하는 함수를 최적화
	const sum = useMemo(() => {
		console.log('합 구하는 중');
		return numbers.reduce((acc, cur) => acc + cur, 0);
	}, [numbers]);
	
	// useCallback을 사용해 addRandomNumber 함수 최적화
	const addRandomNumber = useCallback(() => {
    const randomNumber = Math.floor(Math.random() * 10) + 1;
    setNumbers(prevNumbers => {
	    const updatedNumbers = [...prevNumbers, randomNumber];
	    prevNumbersRef.current = updatedNumbers;
	    return updatedNumbers;
    });
  }, []);
  
  return (
    <div>
      <h2>숫자들의 합: {sum}</h2>
      <button onClick={addRandomNumber}>랜덤 숫자 추가</button>
      <div>이전 숫자들: </div>
      <ul>
	      {prevNumbersRef.current.map((num, index) => (
		      <li key={index}>{num}</li>
	      ))}
      </ul>
    </div>
  );
}
```

### usePromise

> 함수형 컴포넌트에서 Promise를 더 쉽게 사용할 수 있는 hook
> 

```tsx
import React, { useState, useEffect } from 'react';

export default function usePromise(promiseCreator, deps) {
	const [resolved, setResolved] = useState(null);
	const [loading, setLoading] = useState(false);
	const [error, setError] = useState(null);
	
	const process = async () => {
		setLoading(true);
		try {
			const result = await promiseCreator();
			setResolved(result);
		} catch (e) {
			setError(e);
		}
		setLoading(false);
	}
	useEffect(() => {
		process();
	}, deps);
	
	return [loading, resolved, error];
}
```

→ promiseCreator: 프로미스 생성

→ deps: 언제 프로미스를 새로 만들지에 대한 조건
