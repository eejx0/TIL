# API 호출 방법

### 동기식 호출과 비동기식 호출

- 동기식 호출: 자바스크립트 코드가 순차적으로 실행되는 방식
- 비동기식 호출: 자바스크립트 코드가 순차적으로 실행되지 않는 방식

### 비동기식 API 호출 방법

AJAX: 기본적으로 비동기식 API 호출 기술 의미

→ XMLHttpRequest 객체, jQuery 라이브러리의 ajax 함수, Axios 라이브러리, Fetch API

**XMLHttpRequest**: HTTP를 사용해 비동기식 API 호출을 하는데 필요한 여러 기능 제공

open: 통신 초기화, send: 전송 요청, abort: 전송 중지, onreadystatechange: 응답 상태 모니터링

**jQuery.ajax**: 내부적으로 XMLHttpRequest 객체를 사용해 API를 호출하지만 이의 단점을 개선

**Axios**: 비동기식 API를 호출하기 위한 axios 함수 제공

axios: 내부적으로 XMLHttpRequest 객체를 사용하지만 비동기식 API 호출을 간단하게 할 수 있음

```jsx
axios({
	method: 'get',
	url: 'https://api.example.com/data'
})
	.then(response => {
		console.log(response.data);
	})
	.catch(error => {
		console.log(error);
	})
```

**Fetch API**: ****HTTP 프로토콜을 사용해 비동기식 API를 호출할 수 있는 여러 기능 제공

요청에 대한 응답 결과를 Promise 객체로 반환해 편리하게 비동기식 API 호출 가능

```jsx
fetch ("https://api.example.com/data")
	.then((res) => res.text()) // Promise 객체 처리
	.then((success) => console.log(success)) // 성공적으로 API 요청 완료
	.catch((error) => console.log(error)); // API 요청 실패
```

### 비동기식 API 데이터 교환 형식

- CSV: 데이터를 쉼표로 구분해 텍스트 파일 형식으로 저장
- XML: 자바스크립트 기반의 비동기식 API 호출에서 사용하는 데이터 교호나 형식
- JSON: 사람과 기계가 쉽게 읽고 쓸 수 있도록 경량화해 설계한 텍스트 기반의 데이터 교환 형식

### CORS 오류와 대처 방법

> CORS: Cross Origin Resource Sharing (교차 출처 자원 공유)
> 

동일한 출처를 가지고 있을 때만 자원 공유를 허용한다는 sop 보안 정책 때문에 발생하는 오류

**대처 방법**: API 응답에 Access-Control-Allow-Origin 헤더를 포함해 전달

(단 API 응답 조작은 백엔드에서 하므로 프론트에서 직접적으로 할 수 없음)

백엔드의 지원을 받을 수 없는 상황 → 프록시 서버를 사용해 CORS 우회 (완벽한 해결책은 아님)
