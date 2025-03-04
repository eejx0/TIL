# useState를 조건문 안에서 사용하지 못하는 이유
> **리액트가 상태를 관리하는 방식**이 **`useState`**를 **호출하는 순서**와 연관되어 있기 때문
> 

→ 리액트는 `useState()`가 호출된 순서를 기준으로 상태를 저장하고 업데이트

<aside>
❓

**useState를 조건문 안에서 호출하면**

---

- 특정 렌더링 시에는 호출되고 다른 렌더링에선 호출되지 않을 수 있음
- 리액트가 호출 순서를 기반으로 상태를 추적하는 과정에서 혼돈 발생
</aside>

```jsx
const Example = ({ mustUseState }) => {
	if (mustUseState) {
		const [update, setUpdate] = useState(0);
	}
}
```

**mustUseState가 false 일 때** 🤔

useState의 호출 개수가 변경되면서 리액트 내부 상태 저장 방식과 불일치 발생..

렌더링에서 이전에 있던 useState() 호출이 사라지면 다른 호출들이 엇갈려 버그

**useState는 항상 컴포넌트의 최상위에 호출해야한다** 🚨
