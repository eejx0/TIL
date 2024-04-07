### Zustand ?

<aside>
💡 상태 관리 라이브러리

</aside>

### Zustand의 특징

- 특정 라이브러리에 엮이지 x
- 한 개의 중앙 집중된 형식의 스토어 구조 활용
- 상태 정의하고 사용하는 방법이 단순
- Context API와 달리 상태 변경 시 불필요한 리렌더링 일으키지 않도록 제어하기 쉬움
- React에 직접적으로 의존 x → 자주 바뀌는 상태 직접 제어 방법 제공

### Zutand 설치

`npm install zustand`

`yarn add zustand`

### Zustand 사용

**Store 생성**

```jsx
import create from 'zustand';

const useMemosStore = create((set) => (
	memo: '',
	setMemo: (text) => set({ memo: text }),
	memos: [],
	setMemos: (newMemo) => 
		set((prev) => ({
			memos: [..prev.memos, newMemo],
		})),
))
```

→ memo, memos엔 초기값을 넣음

→ setMemo, setMemos는 매개변수를 지정하고 어디에 어떻게 값을 넣을지 정함

→ setMemo일 때 text라는 값이 들어오면 memo에 text를 넣음

→ setMemos의 경우 memos의 새로운 값인 newMemo를 추가해야 함

→ prev 매개변수 사용

→ 스프레드 연산자를 사용할 때 prev.memos처럼 뒤에 타겟이 되는 배열명을 넣어야 함
