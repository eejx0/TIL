## useMemo

### 역할

<aside>
💡

**컴포넌트의 성능 최적화**에 사용되는 훅

</aside>

**memo**
프로그램이 동일한 계산을 반복해야 할 때 이전에 계산한 값을 메모리에 저장함으로써 동일한 계산의 반복 수행을 제거해 실행 속도를 빠르게 하는 기술

```jsx
function Component() {
	const value = nurung();
	return <div>{value}</div>
}

function nurung() {
	return 10;
}
```

> 처음에 **계산된 값을 메모리에 저장**해 컴포넌트가 **계속 렌더링**되어도 nurung을 **다시 호출하지 않**고 메모리에 저장되어있는 **계산된 값을 가져와 재사용**
> 

**useMemo를 사용하지 않으**면

렌더링 → 컴포넌트 함수 호출 → **모든 내부 변수 초기화**
nurung이 복잡한 함수라면 비효율적일 것..

**useMemo를 사용**하면

렌더링 → 컴포넌트 함수 호출 → **memorize된 함수 재사용**
nurung 함수를 반복적으로 실행할 필요 x

### 구조

```jsx
const value = useMemo(() => {
	return nurung();
}, [item])
```

### useCallback와 차이점

> useMemo와 useCallback은 **Memoization이란 기술**을 사용한 hook으로 **최적화**를 위해 사용 ⭐
> 

**useMemo**

**Memoization된 값**을 반환하는 함수

**useCallback**

**Memoization된 함수**를 반환하는 함수

## useEffect

### useEffect에서 함수를 반환하면?

<aside>
💡

**CleanUp function**으로 동작

</aside>

React가 컴포넌트를 언마운트하거나 useEffect가 다시 실행되기 전에 
리소스를 정리하기 위한 매커니즘 제공

### 두 번째 인자 적용 방법 (3가지)

1. **빈 배열 ([]) 전달**
    
    > **컴포넌트가 처음 마운트**될 때만 실행
    > 
    - 컴포넌트가 마운트 될 때만 실행되고 이후에 다시 실행되지 않음
    - 언마운트 시에만 클린업 함수가 호출됨
    - 해당 useEffect는 한 번만 실행
2. **특정 값이 변경될 때만 실행 ([value1, value2])**
    
    > **배열에 포함된 값이 변경**될 때마다 실행
    > 
    - 배열에 들어있는 값이 변경되지 않으면 useEffect는 실행되지 않음
3. **디펜던시 배열을 생략하는 방법**
    
    > **컴포넌트가 렌더링**될 때마다 실행
    > 
    - 상태나 props가 변경될 때마다 useEffect가 다시 호출됨
    - 렌더링 시점마다 작업을 수행해야 할 때 사용

### clean up function

<aside>
💡

useEffect Hook 내에서 return되는 함수

</aside>

→ 컴포넌트가 사라질 때 (언마운트), 특정 값이 변경되기 직전에 실행할 작업 지정 가능

```jsx
useEffect(() => {
	// mount, deps update 시점에 실행할 작업 (componentDidMount)
	return () => {
		// unmount, deps update 직전에 실행할 작업 (componentWillUnmount)
	}
}, [deps]);
```
