# useContext

> 기존 react에 존재하는 **Context를 더 편하게 사용**할 수 있게 해주는 역할
> 

### Context ?

데이터가 필요할 때마다 props를 통해 전달할 필요 x

👉🏻 context 이용해 공유

- createContext: context 객체 생성
- Provider: 생성한 context를 하위 컴포넌트에게 전달
- Consumer: context의 변화 감시

### useContext의 필요성

App.js

```jsx
import react, {createContext} from "react";
import Children from "./Children";

export const AppContext = createContext();

const App = () => {
	const user = {
		name: "신예찬",
		job: "밴드"
	};
	
	return (
		<>
			<AppContext.Provider value={user}> 
				<div>
					<Children />
				</div>
			</AppContext.Provider>
		</>
	);
};

export default App;
```

Children.js → context 적용

```jsx
import React from "react";
import {AppContext} from "./App";

const Children = () => {
	return (
		<AppContext.Consumer>
			{(user) => (
				<>
					<h3>AppContext에 존재하는 값의 name은 {user.name}입니다.</h3>
          <h3>AppContext에 존재하는 값의 job은 {user.job}입니다.</h3>
				</>
			)}
		</AppContext.Consumer>
	);
};

export default Children;
```

Children.js → useContext 적용

```jsx
import React, {useContext} from "react";
import {AppContext} from "./App";

const Children = () => {
	const user = useContext(AppContext);
	return (
    <>
      <h3>AppContext에 존재하는 값의 name은 {user.name}입니다.</h3>
      <h3>AppContext에 존재하는 값의 job은 {user.job}입니다.</h3>
    </>
  );
};

export default Children;
```

> useContext를 사용하면 Context 보다 더 쉽게 Context 사용 가능
useState, useEffect와 조합해 사용하기 쉬움 👍🏻
>
