# 웹 소켓 (Web Socket)
### 🗣 웹 소켓 (Web Socket)

---

> **웹 앱과 서버 간의 지속적인 연결을 제공하는 프로토콜** ✅
> 

서버와 클라이언트 간의 양방향 통신이 가능해짐
WebSocket 연결은 한 번 열린 후 계속 유지되므로 서버나 클라이언트에서 언제든지 데이터를 전송할 수 있음

→ **실시간 통신**에서 적극 사용

<aside>
🔥

**실시간 웹 애플리케이션을 위해 설계된 통신 프로토콜**

---

- TCP를 기반으로 함
- 신뢰성 있는 데이터 전송을 보장하고 메시지 경계를 존중
- 순서가 보장된 양방향 통신 제공 (양쪽에서 모두 정보를 주고받을때 데이터는 패킷 형태로 전달되고 전송은 연결 중단과 추가 HTTP 요청 없이 양방향으로 이루어짐)
</aside>

### 🗣 등장 배경

---

**초기의 인터넷 통신 방식**

- 클라이언트가 서버에 요청을 보내고 서버가 이에 응답
- 클라이언트가 서버에게 요청하지 않는 이상 서버는 클라이언트에게 먼저 데이터를 보낼 수 없음
- 클라이언트는 항상 새로운 데이터가 있는지 확인 하기 위해 서버에 지속적으로 요청을 보내야 함
- 불필요한 트래픽 ⬆️
- 서버 비용 ⬆️
- 요청과 응답 사이의 지연시간 때문에 실시간 통신의 효율성 ⬇️

→ 이런 상황을 해결하기 위해 사용하는 것이 **`웹 소켓`**

### 🗣 연결하는 방식

---

클라이언트 환경에선 별도의 패키지 설치 없이 브라우저 자체에서 web Socket API 지원 

→ new 웹소켓만 호출해 사용하면됨 (ws 라는 특수 프로토콜 사용)

```tsx
const socket = new WebSocket("wss://example/chat");
```

소켓 이벤트

- **open**: 연결이 성공적으로 되었을 때 발생
- **message**: 데이터를 수신했을 때 발생
- **error**: 연결 상 에러가 생겼을 때 발생
- **close**: 연결이 종료되었을 때 발생

```tsx
let socket = new WebSocket("wss://example/chat");
// 이렇게 소켓을 생성하면 즉시 연결이 시작됨

socket.onopen = function(e) {
	// [open] 커넥션이 만들어짐
	socket.send("안뇽") 
} 

socket.onmessage = function(event) {
	console.log(`${event.data}`); // [message] 서버로부터 전송받은 데이터가 출력됨
}

socket.onclose = function(event) {
	if (event.wasClean) {
		console.log(`code=${event.code} reason=${event.reason}`); // [close] 커넥션 종료
	} else {
		console.log("[close] 커넥션이 죽음") // ex: 프로세스가 죽거나 네트워크에 장애가 있는 경우
		// event.code가 1006이 됨
	}
}

socket.onerror = function(error) {
	alert(`[error]`)
}
```

### 🗣 handshake

---

`new WebSocket("wss://example/chat")` 을 호출해 최초 요청을 전송하면 요청 헤더는

```
GET /chat
Host: example
Origin: https://example
Connection: Upgrade
Upgrade: websocket
Sec-WebSocket-Key: Iv8io/9s+lYFgZWcXczP8Q==
Sec-WebSocket-Version: 13
```

**Origin**: 클라이언트의 Origin

**Connection**: 클라이언트 측에서 프로토콜을 바꾸고 싶다는 신호를 보냈다는 것

**Upgrade**: 클라이언트 측에서 요청한 프로토콜은 websocket이라는걸 의미

**Sec-WebSocket-Key**: 보안을 위해 브라우저에서 생성한 키

→ 서버가 웹소켓 프로토콜을 지원하는지 확인하는 데 사용됨

**Sec-WebSocket-Version**: 웹소켓 프로토콜 버전

서버가 해당 요청을 받으면 웹 소켓 연결을 수락하는 이런 응답을 보냄

```
101 Switching Protocols
Upgrade: websocket
Connection: Upgrade
Sec-WebSocket-Accept: hsBYongNyong24s99EO10UlZ22C2g=
```

→ 클라이언트와 서버 간 실시간 통신이 가능한 통로가 열림

→ 클라이언트와 서버 간에 실시간 양방향 통신이 가능해짐

### 🗣 한계점

---

- 웹 소켓은 HTML5 사양의 일부라 HTML5를 지원하지 않는 브라우저에선 사용 ❌
- 웹 소켓은 한번 연결되면 별도의 에러, 지시가 없는 한 지속적인 연결을 유지하므로 많은 웹 소켓 연결을 동시에 관리하는 경우 서버의 부하 ⬆️
- 연결이 끊어졌을 시 웹소켓은 연결이 끊긴 이유에 대해 정확히 알 수 없으므로 그에 대한 에러 처리도 쉽지않음
