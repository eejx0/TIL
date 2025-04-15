# Fetch vs Axios
> 🗣: fetch 대신 axios를 따로 설치해서 사용한 이유가 뭔가요?
👩🏻: 어.. 사실 주변 선배들과 친구들이 axios가 더 좋다고 그래서 따라 사용한거긴 합니다..
> 

**Fetch**

- fetch()를 통해 HTTP 요청과 응답을 JS에서 접근, 조작할 수 있는 인터페이스를 제공
- 최신 브라우저에 내장되어 있어 따로 설치할 필요 ❌

**Axios**

- CDN이나 npm/yarn 등을 통해 설치해야함
- 브라우저나 node.js 환경 내에서 실행됌

## 비교

### 문법

**Fetch**

- 2개의 인자를 받음
- 첫번째 인자는 자원을 얻어오고자하는 URL
- 두번째 인자는 optional로 요청을 만드는데에 필요한 설정이 들어있는 객체
    
    ```tsx
    fetch(url, {
    	method: 'GET',
    	headers: {
    		'Content-Type': 'application/json'
    	}
    })
    ```
    

**Axios**

- 기본적으로 GET 요청을 보냄
- fetch랑 아에 같은 문법을 사용하는 것도 가능
- 모든 옵션을 객체로 만들어 인자로 넘기는 것도 가능
    
    ```tsx
    axios({
    	method: 'get',
    	url: url,
    	headers: {}
    })
    ```
    

### JSON data

**Fetch**

- .then() 메서드를 사용해 응답 결과를 다뤄야하는 promise 리턴
- Response 객체에서도 필요한건 http 응답 전체가 아닌 json 본문이기 때문에 이를 추출하기 위해선 .json() 메서드를 호출해야 함
- json으로 파싱하기 위해 또 다른 promise가 리턴되면 결국 최소 두개의 .then() 체인 사용
    
    ```tsx
    fetch(url)
    	.then(res => res.json())
    	.then(console.log)
    ```
    

**Axios**

- 응답 데이터가 JSON 형식을 기본값으로 사용
- 응답 결과는 항상 응답 객체의 data 속성에서 찾을 수 있음
    
    ```tsx
    axios.get(url)
    	.then(res => console.log(res.data));
    ```
    
- response 타입을 따로 명시도 가능

### 자동 문자열화

**Fetch**

- request body에 데이터를 할당하기 위해 JSON.stringify() 필요
- Content-Type을 application/json으로 명시
    
    ```tsx
    fetch(url, {
    	method: 'POST',
    	headers: {'Content-Type': 'application/json'},
    	body: JSON.stringify(data)
    });
    ```
    

**Axios**

- 그냥 설정 옵션 객체의 data 속성에 보내고 싶은 데이터를 넣어주면 됌
    
    ```tsx
    axios.post(url, {
    	headers: {
    		'Content-Type': 'application/json'
    	},
    	data: data
    })
    ```
    

### 에러 핸들링

**Fetch**

- fetch가 반환하는 promise는 200번이 아닌 status code를 받아도 reject되지 않음
    
    → 그럼 언제 reject됨 🤔
    
    네트워크 연결이 실패하거나 해서 아예 요청을 보내지 못했을 경우..
    
- 코드가 뭐든 fetch()입장에선 요청을 보냈고 응답을 받은 거임
- status code가 200번대가 아닐 경우 ok 속성이 false로 설정
- ok 상태를 이용해 별도로 에러 핸들링

**Axios**

- axios의 promise는 200번대가 아니면 반드시 reject됨
- fetch와 다르게 별도의 에러 처리 과정 필요 없이 바로 .catch() 구문에서 처리 가능
    
    ```tsx
    axios.get(url)
    	.then((res) => console.log(res.data))
    	.catch((err) => {
    		console.log(err.message);
    	})
    ```
    

### 성능

Fetch가 조금 더 빠름
