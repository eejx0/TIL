# Zustand

<aside>
💡 **최소한의 코드**로 **상태 관리**❗

</aside>

## 개념

> 독일어로 ‘**상태**’ 라는 뜻
> 

➡️ **쓰기 쉽고 간단한 코드**만 필요하며 **Redux Devtools 사용**이 가능해 **디버깅에도 용이**

## 사용법

### 1. Zustand 설치

```bash
npm i zustand # or yarn add zustand
```

### 2. store 생성

```jsx
// store.js

import create from 'zustand' // create로 zustand를 불러옴

const useStore = create(set => ({
	bears: 0,
	increasePopulation: () => set(state => ({ bears: state.bears + 1})),
	removeAllBears: () => set({ bears: 0 })
}))

export default useStore
```

🔍 bears라는 초기값 선언

그 값을 조작하는 increasePopulation(bears를 1씩 증가)과

removeAllBears(bears를 0으로 리셋)를 선언함 → set 이용

### 3. store에 생성한 useStore 불러와서 사용
