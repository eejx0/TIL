# useREf

<aside>
💡 저장공간 또는 DOM 요소에 접근하기 위해 사용되는 React Hook

</aside>

ref: 참조

- 자바스크립트 → 특정 DOM 선택: querySelector 등 함수 사용
- React → 특정 DOM 선택: useRef라는 React Hook 사용
- useRef로 관리하는 값은 값이 변해도 화면에 렌더링 되지 않음

```tsx
import React, { useRef } from "react";

function MyComponent() {
	const inputRef = useRef<HTMLInputElement>(null);

	const focusInput = () => {
		if (inputRef.current) {
			inputRef.current.focus();
		}
	};

	return (
    <div>
      {/* input 요소에 ref 속성에 inputRef를 할당하여 참조를 설정합니다. */}
      <input type="text" ref={inputRef} />
      {/* 버튼을 클릭하면 focusInput 함수가 호출됩니다. */}
      <button onClick={focusInput}>Input에 포커스 주기</button>
    </div>
  );
}
```
