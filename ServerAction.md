# Server Action
> **서버에서 실행되며 브라우저에서 호출할 수 있는 비동기 함수**
> 

→ Next.js에서 제공하는 기능

→ **서버 로직을 직접 호출함**으로써 **클라이언트와 서버 간의 상호작용을 간소화**할 수 있게 해줌

ex) 백엔드 서버와 api 통신을 하는 대신 next 서버에서 디비에 직접 접근하는 식으로 활용 가능

### 사용 방법 💬

```tsx
"use server";

export async function addTodo(todo: string) {
	console.log("예제", todo);
	return { success: true };
}
```

```tsx
"use client";

export default function TodoList() {
	const [input, setInput] = useStatE("");
	
	const handleSubmit = async () => {
		if (!input) return;
		const result = await addTodo(input);
		console.log(result);
		setInput("");
	};
	
	return (
		<div>
			<input value={input} onChange={(e) => setInput(e.target.value)}/>
			<button onclick={handleSubmit}>추가</button>
		</div>
	)
}
```

### 장점

<aside>
🔥

**클라이언트와 서버 간 상호작용을 간소화 가능**

---

- 기존엔 디비와 관련된 처리를 위해 백엔드 api와 통신하는 방식 사용
- server action으로는 백엔드와 통신을 하지않고 next 서버에서 직접 디비 작업 수행
- 개발 생산성 ⬆️
- 네트워크 통신을 줄여 성능 ⬆️
</aside>

<aside>
🔥

**Server Action 로직은 클라이언트에게 전송되지 않음**

---

- 보안에 도움
- 외부에 노출되면 안되는 정보다 로직을 숨기는데 도움
- 클라이언트 단의 일부 로직을 Server Action으로 옮기면 번들의 크기 ⬇️
</aside>

<aside>
🔥

**JS가 로드되기 이전의 시점에도 서버와 상호작용 가능**

---

- Server Action은 html <form>의 action 속성을 이용해 폼 데이터를 서버에 전송
- JS가 로드되지 않거나 비활성화되어도 서버와 통신이 가능
</aside>
