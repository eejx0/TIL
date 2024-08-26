## 태스크 큐

> **마이크로태스크 큐**와 **매크로태스크 큐**(일반 태스크큐)로 나뉨
> 

→ 둘 다 콜백 함수나 이벤트 핸들러를 일시 저장함

→ microtask queue 👉🏻 Promise

→ task queue, macrotask queue 👉🏻 setTimeout, setInterval

**차이점**

- 태스크 큐보다 마이크로태스크 큐의 우선순위가 더 높음
- 이벤트 루프는 콜 스택이 비면 먼저 마이크로태스크 큐에서 대기하고 있는 함수 실행
- 마이크로태스크 큐가 비면 태스크 큐에 대기하고 있는 함수 실행

## 실행 컨텍스트

### 정의

<aside>
⚙ **실행 가능한 코드**에 제공할 **환경 정보를 모아놓은 객체**

</aside>

→ 객체엔 변수 객체, 스코프 체인, this 정보가 담겨있음

### 동작 방법

1. 자동으로 전역 컨텍스트 생성됨
2. 함수 호출시마다 함수 컨텍스트가 생성됨
3. 컨텍스트 생성 완료 후에 함수가 실행됨
4. 함수 실행 중 사용되는 변수들은 변수 객체 안에서 값 찾음
5. 값이 존재하지 않으면 Scope 체인을 따라 올라가면서 탐색
6. 함수 실행이 마무리되면 해당 컨텍스트는 사라짐
7. 페이지가 종료되면 전역 컨텍스트도 사라짐

## 함수형 컴포넌트와 클래스형 컴포넌트 차이

### 일반적인 차이

**클래스형**

- state와 lifeCycle API 사용 가능
- 임의 메서드 정의 가능

**함수형**

- state와 lifeCycle API 사용 가능 (Hook으로 해결 가능)
- 클래스형 컴포넌트보다 선언하기 편함
- 메모리 자원을 덜 사용
- 빌드한 결과물의 크기가 더 작음

### 선언 방식의 차이

**클래스형**

```jsx
import React, {Component} from "react";

class App extends Component {
	render() {
		const text = '안녕'
		return <div className=react>{text}</div>
	}
}

export default App;
```

- class 키워드 필요
- componenet를 상속받아야함
- 화면에 표시하기 위한 render() 메서드가 반드시 필요

**함수형**

```jsx
import React from "react";

const App = () => {
	const text = '안녕'
	return <div className="react">{text}</div>
}
```

- 함수 자체가 렌더 함수라 render() 메서드 사용하지 않아도 됨
- component 상속받지 않아도 됨

### State 사용 차이

**클래스형**

```jsx
constructor(props) {
	super(props);
	
	this.state = {
		name: 'eejx0',
		items: []
	}
}

// constructor 없이 사용하는 법
class App extends Component {
	state = {
		naem: 'eejx0'
		items: []
	}
}
```

- constructor 안에서 this.state로 초기 값 설정 가능
- constructor 없이도 초기 값 설정 가능
- 클래스형 컴포넌트의 state는 객체 형식
- this.setState 함수로 state 값 변경 가능 → ex) `this.setState({ price: price + 10 });`

**함수형**

```jsx
const App = () => {
	const [name, setName] = useState('eejx0');
	
	const onClick = {() => {
		setName('euijin');
	}}
}
```

- useState로 state 핸들링
- useState 함수 호출 시 배열이 반환됨
- 첫 번째 원소는 state, 두 번째 원소는 state를 변경해주는 함수
- useState의 파라미터는 state의 초기값

### Props 사용 차이

**클래스형**

```jsx
class App extends Component {
	render() {
		const {name, age} = this.props;
		return (
			<div>
				난 {name}이고 {age}살이야
			</div>
		)
	}
}
```

- this.props로 불러옴

**함수형**

```jsx
const App = ({name, age}) => {
	return (
		<div>
			난 {name}이고 {age}살이야
		</div>
	)
}
```

- 랜더함수의 parameter로 props 전달받아 사용

### LifeCycle 차이

컴포넌트는 생성(mount) → 업데이트(update) → 제거(unmount)의 생명주기를 가짐

**클래스형**

- LifeCycle API는 클래스형 컴포넌트에서 활용되는 것
- 컴포넌트가 DOM 위에 생성되기 전과 후의 데이터가 변경되어 상태를 업데이트하기 전과 후로 실행되는 메서드들

**함수형**

- 리액트 hook
    - 함수형 컴포넌트에서 React state와 생명주기 기능을 연동할 수 있게 해주는 함수들
    - 클래스형 컴포넌트에선 동작 x
    - class 없이 React를 사용할 수 있게 해줌

### 이벤트 핸들링

**클래스형**

```jsx
handleClick = e => {...}

render() {
	return (
		<input type="button" onClick={this.handleClick}>버튼</input>
	)
}
```

- 함수 선언 시 애로우로 바로 선언 가능
- 적용하기 위해선 this 붙여야 함

함수형

```jsx
const handleClick = () => {...}

return (
	<input type="button" onClick={this.handleClick}>버튼</input>
)
```

- const 함수 형태로 선언해야 함
- this 필요 없음

## Babel과 webpack

### Babel

> 대표적인 **트랜스 파일러**
> 

트랜스파일링: 특정 언어로 작성된 코드를 비슷한 다른 언어로 변환시키는 것

**설치**

`npm install --save-dev @babel/core @babel/cli` 

```json
"devDependencies": {
    "@babel/cli": "^7.18.10",
    "@babel/core": "^7.19.0"
 }
```

바벨 사용하려면 @babel/preset-env 설치해야 함 →  `npm install --save-dev @babel/preset-env`

@babel/preset-env

- 함께 사용되어야 하는 바벨 플러그인을 모아 둔 것, 바벨 프리셋이라고 부름
- 필요한 플러그인들을 프로젝트 지원 환경에 맞춰 동적으로 결정해줌

설치 완료 시 루트 폴더에 babel.config.json 설정 파일 생성

```json
{
	"presets": ["@babel/preset-env"]
}
```

**Babel 플러그인 설치**

if) @babel/plugin-proposal-class-properties 설치

`npm install --save-dev @babel/plugin-proposal-class-properties` 

설치한 플러그인은 babel.config.json에 추가해야 함

```json
{
	"plugin": ["@babel/plugin-proposal-class-properties"]
}
```

### Wepack

> **모듈 번들러**
> 

코딩할 때 편의를 위해 모듈로 나눠 작업하는 경우가 많지만 이렇게 하면 많은 네트워크 비용 낭비 → 여러 모듈을 하나의 파일로 묶어 보내자!!

- 의존 관계에 있는 js, css 이미지 등의 리소스들을 하나의 파일로 번들링
- 의존 모듈이 하나의 파일로 번들링되므로 별도의 모듈 로더 필요 x
- 여러개의 js 파일을 하나로 번들링해 html 에서 script 태그로 js 파일 로드해야하는 번거로움 사라짐

**설치**

`npm install --save-dev webpack wepack-cli` 

웹팩이 모듈 번들링 할 때 바벨로 es5 사양의 소스코드로 트랜스 파일링 하도록 babel-loader 설치

`npm install --save-dev babel-loader`

webpack.config.json 설정 파일 작성

```jsx
const path = require("path");

module.exports = { 
	entry: "./src/js/main.js" // 번들링된 js 파일의 이름과 저장될 경로 지정
	output: {
		path: path.resolve("dist"),
		filename: "[name].js",
	},
	module: {
		rules: [
			test: /\.css$/, // .css 확장자로 끝나는 모든 파일
			use: ["css-loader"], // css loader 적용
		]
	}
}
```
