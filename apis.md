# API의 종류

### 브라우저 API

<aside>
💡 웹 브라우저에서 자체적으로 제공하는 API 집합

</aside>

→ 웹 브라우저의 다양한 기능과 인터페이스 제어를 위해 사용

**DOM API**: 개발자가 HTML 문서의 구조와 내용에 접근해 조작할 수 있는 방법 제공

- 요소 선택과 탐색: HTML 문서의 특정 요소 선택 가능 (getElementById, querySelector …)
- 요소 생성과 조작: innerHTML, innerText, createElementm, setAttribute …
- 문서 조작: 문서 자체의 구조 제어 (appendChild, removeChild, replaceChild …)
- 이벤트 처리: 이벤트에 해당하는 이벤트 리스너 등록해 특정 기능 동작

**지오로케이션 API**: 사용자의 위치 정보 가져오는 기능 제공

→ 사용자의 현재 위치를 파악함으로써 사용자 위치 기반 서비스 개발 가능

```jsx
const myElement = document.getElementById("demo");
function getLocation() {
	if (navigator.geolocation) {
		navigator.geolocation.getCurrentPosition(showPosition);
	} else {
		myElement.innerHTML = "Geolocation";
	}
}
function showPosition(position) {
	myElement.innterHTML = "Latitude: " + position.coords.latitude + 
												 "<br>Logitude: " + position.coords.longitude;
}
```

**스토리지 API**: 데이터를 웹 브라우저에 저장하는 방법 제공

- 웹 스토리지 API: 키-값 형태의 데이터를 사용자의 웹 브라우저에 저장하는 API
    
    로컬 스토리지: 웹 브라우저를 종료해도 데이터가 유지됨 (EX: 아이디 저장 기능)
    세션 스토리지: 웹 브라우저가 종료되면 데이터도 같이 삭제됨 (EX: 사용자 인증 정보)
    
    ```jsx
    localStorage.setItem('myData', 'Hello Word');
    // 로컬 스토리지에 키-값 형태로 데이터 저장
    const data = localStorage.getItem('myData');
    // 로컬 스토리지에 저장된 데이터 가져오기
    console.log(data);
    ```
    
- 인덱스드DB API: 웹 브라우저에 데이터에 저장하기 위한 고급 메커니즘 제공
    
    데이터를 고정되지 않은 객체 형태로 웹 브라우저에 저장 → 저장된 데이터는 별도로 삭제하지 않는 이상 웹 브라우저에 영구적으로 존재
    
    - 코드
        
        ```jsx
        const request = indexedDB.open('myDB');
        // 데이터베이스 열기
        request.onerror = function (e) {
        	console.log('error: ' + e.target.errorCode);
        };
        
        request.onsuccess = function (e) {
        	const db = e.target.result;
        	// 데이터베이스 객체 가져오기
        	const transaction = db.transaction(['myStore'], 'readwrite');
        	const store = transaction.objectStore('myStore');
        	store.add({ id: 1, data: 'First Data' });
        	// 스토어에 데이터 저장
        	const request = store.get(1);
        	request.onsuccess = function (e) {
        		const data = e.target.result;
        		console.log(data); // 출력: {id: 1, data: 'First Data'}
        	};
        	// 스토어에서 id의 값이 1인 데이터 검색
        };
        
        request.onupgradeneeded = function (e) {
        	const db = e.target.result;
        	db.createObjectStore('myStore', { keyPath: 'id' });
        	// myStore라는 객체 스토어 생성 후 keyPath를 id로 지정
        };
        // 데이터베이스 버전 업그레이드가 필요한 경우
        ```
        
- 서드파티 API: 개인이나 기업의 이윤 창출을 위해 만들어진 API
    
    구글, 페이스북, 인스타그램, 카카오 등에서 제공하는 API
    공개 API (open API, public API), 내부 API (internal API, private API), 파트너 API
