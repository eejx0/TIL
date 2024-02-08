# api 연동 정리

## 호출 방법

### fetch

> Javascript의 네트워크 요청을 위한 내장 함수로 별도의 설치없이 사용 가능
JSON 객체를 얻기 위해선 .then()을 2번 사용해야 함
> 

```jsx
const API함수 = () => {
	fetch("API 주소")
		.then((res) => res.json())
		.then((data) => console.log(data))
		.catch((err) => console.log(err))
}
```

### axios

> npm, yarn에서 설치 해 사용 가능
바로 JSON 객체를 내뱉어 편하게 사용 가능하고 보안상의 이점이 있음
> 

npm install axios & yarn add axios 

```jsx
import axios from "axios";

const API함수 = () => {
	axios
		.get("API 주소")
		.then((data) => console.log(data))
		.catch((err) => console.log(err))
}
```

### async/await + fetch

> .then() 안쓰고 비동기 코드를 동기적으로 표현 가능
> 

```jsx
const API함수 = () => {
	try {
		const res = await fetch("API주소");
		const data = await res.json();
		console.log(data);
	} catch (err) {
		console.log(err);
	}
};
```

### async/await + axios

> 보편적인 방법
> 

```jsx
import axios from "axios";

const API함수 = async () => {
	try {
		const res = await axios.get("API주소");
		console.log(res.data);
	} catch (err) {
		console.log(err);
	}
};
```
