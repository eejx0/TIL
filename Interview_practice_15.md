## useEffect

### 정의

<aside>
💡 **React Component**가 **렌더링** 될 때마다 **특정 작업을 실행**할 수 있도록 하는 **Reack hook**

</aside>

### 사용 방법

`useEffect(func, deps)`

→ **func**

수행하고자 하는 작업 (리액트는 이 함수를 기억했다가 dom 업데이트 후 불러냄)

이 함수에서 함수 return 시 그 함수가 컴포넌트가 Unmount 될 때 다시 실행됨

→ **deps**

배열 형태로 배열 안엔 검사하고자 하는 특정 값 or 빈 배열

특정 값을 넣게 되면 컴포넌트가 mount 될 때 지정한 값이 업데이트 될 때 useEffect 실행

### 사용 방식

**componentDidMount**

component가 mount 됐을 때 (처음 나타났을 때 실행)

```jsx
useEffect(() => {
	console.log("마운트 될 때 실행");
}, []);
```

```jsx
useEffect(() => {
	console.log("렌더링 될 때 실행");
});
```

**componentDidUpdate**

component가 update될 때 (특정 props, state가 바뀔 때 실행)

```jsx
useEffect(() => {
	console.log(age);
	console.log('업데이트 될 때 실행');
}, [age]);
```

```jsx
const mounted = useRef(false);
useEffect(() => {
	if (!mounted.current) {
		mounted.current = true;
	} else {
		console.log(age);
		console.log("업데이트 될 때 실행");
	}
}, [age])
```

## useRef

### 정의

<aside>
💡

**저장공간** 또는 **DOM 요소에 접근**하기 위해 사용되는 **React Hook**

</aside>

→ JS에선 특정 DOM을 선택하기 위해 querySelector 함수 사용

→ React에선 DOM을 선택해야 할 때 useRef라는 React Hook 사용

### 사용 예시

```jsx
const Mycomponent = () => {
	const inputRef = useRef(null);
	
	useEffect(() => {
		inputRef.current.focus();
	}, [])
}

return (
	<div>
		<input ref={inputRef} type="text"/>
	</div>
)
```

### 언제 사용

- DOM 요소에 직접 접근해야 할 때 (ex: 어떤 특정한 입력 필드에 포커스를 설정해야 할 때)
- 컴포넌트가 리렌더링되어도 변경되지 않는 값을 저장해야할 때
- setTimeout, setInterval 등의 참조를 유지하고자 할 때

## container와 component의 차이

### Component 파일

> 그래픽적으로 **화면을 구성하는 UI 요소**를 정의
> 

→ 화면에서 보여지는 부분

ex: 버튼, 폼, 카드 등의 화면 요소

```jsx
import React from "react";

export const SearchForm = ({ handleSubmit }) => (
	<from onSubmit={handleSubmit}>
		<input type="text" value={searchTerm} onChange={handleChange} />
    <button type="submit">Search</button>
	</form>
)
```

### Container 파일

> **UI 요소와 상태 로직을 연결**하는 역할
> 

→ 뒷단에서의 데이터 관리 부분

ex: 폼에서 입력된 데이터 처리, API 호출 수행 등의 상태 관리 역할

```jsx
import React, { useState } from 'react';
import SearchForm from './SearchForm';

const SearchFormContainer = () => {
  const [searchTerm, setSearchTerm] = useState('');

  const handleSubmit = e => {
    e.preventDefault();
    console.log(`Searching for: ${searchTerm}`);
  };

  const handleChange = e => {
    setSearchTerm(e.target.value);
  };

  return (
    <SearchForm
      handleSubmit={handleSubmit}
      handleChange={handleChange}
      searchTerm={searchTerm}
    />
  );
};
```

## React Hook

### 정의

<aside>
💡

**함수 컴포넌트**에서 **React state와 생명주기 기능을 연동**할 수 있게 해주는 함수

</aside>

→ 리액트 v16.8에 도입된 기능

### 특징

- 더 빠른 성능과 짧은 코드의 양
    - 클레스형 컴포넌트에선 라이프 사이클 이용 시 componentDidMount, componentDidUpdate, componentWillWunmount 모두 다르게 처리
    - react hook에선 useEffect 안에서 모두 처리
- 컴포넌트로부터 상태 관련 로직 추상화 가능
    - 이를 통해 독립적인 테스트와 재사용 가능
- 호출되는 순서에 의존
    - 반복문, 조건문, 중첩된 함수 내에서 호출 불가
- 클로저에 의존적
    - 프로그램이 커질수록 hooks가 많아지는데 클로저는 복잡성을 증가시킴

### class 컴포넌트와 차이점

> **class 컴포넌트**
> 

```jsx
import React, {Component} from "react";

class Component extends Component {
	constructor(props) {
		super(props);
		this.state = {
			count: 0
		}
	}
	componentDidMount() {
		console.log('컴포넌트 마운트')
	}
	componentDidUpdate() {
		console.log('컴포넌트 업데이트')
	}
	componentWillUnmount() {
		console.log('컴포넌트 언마운트')
	}
	inrement = () => {
		this.setState({count: this.state.count+1});
	};
	
	render() {
		return (
			<div>
				<p>Count: {this.state.count}</p>
				<button onClick={this.increment}>Increment</button>
			</div>
		)
	}
}
```

> **hooks**
> 

```jsx
import React, {useState, useEffect} from "react";

function Component() {
	const [count, setCount] = useState(0);
	
	useEffect(() => {
		console.log('컴포넌트 마운트');
		return () => {
			console.log('컴포넌트 언마운트');
		}
	}, [count]);
	
	const increment = () => {
		setCount(count + 1);
	};
	
	return (
		<div>
      <p>Count: {count}</p>
      <button onClick={increment}>Increment</button>
    </div>
	)
}
```

### 최상단에 작성해야하는 이유

> **React Hook의 규칙**에 따라야 하기 때문
> 
- hooks는 순서대로 호출되어야 함
    - 컴포넌트가 렌더링될 때마다 React는 각 hook이 호출되는 순서 기억
    - 그 순서에 따라 해당 hook의 상태를 유지하고 업데이트
- 조건문 안에서 hook 호출의 문제
    
    ```jsx
    if (count > 0) {
    	console.log('조건문 안에서 hooks 호출 불가')
    } // 이렇게 쓰면 안됌!
    ```
    
- 코드의 일관성과 예측 가능성 유지
- react의 컴파일 타임 최적화
