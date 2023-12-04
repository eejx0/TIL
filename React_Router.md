# React[Router]

- Switch 대신 Routes

- Switch의 네이밍 Routes로 변경
- exact 옵션 삭제
- component 방식 변경
- path를 기존의 path=”/Web/:id”에서 path=”:id”로 상대 경로로 지정
- 이 외에도 path=”.” / path=”..”등으로 상대경로 표현

**기존 v5의 방식**❓

```jsx
import { BrowserRouter, Route, Switch } from "react-router-dom";
import Home from "./pages/Home";
import Write from "./pages/Write";

function App() {
  return (
    <BrowserRouter>
      <Switch>
        <Route path="/" component={() => <Home />} />
        <Route exact path="/write" component={() => <Write />} />
        <Route component={() => <div>Page Not Found</div>} />
      </Switch>
    </BrowserRouter>
  );
}

export default App;
```

Switch를 사용
exact로 복수의 라우팅 막음
component={} 내에 arrow function을 사용해 component를 전달함

**v6 방식**❗

```jsx
import React from "react";
import { BrowserRouter, Route, Routes } from "react-router-dom";
import { Main, Page1, Page2, NotFound } from "../pages";
import { Header } from ".";

const Router = () => {
	return (
		<BrowserRouter>
			<Header />
			<Routes>
				<Route path="/" element={<Main />} />
				<Route path="/page1/" element={<Page1 />} />
				<Route path="/page2/" element={<Page2 />} />
				<Route path="/*" element={<NotFound />} />
			</Routes>
		</BrowserRouter>
	);
};

export default Router;
```

exact는 더이상 사용하지 않고 여러 라우팅 매칭하고 싶은 경우 url 뒤에 * 사용
component 대신 element로 바로 component를 전달
