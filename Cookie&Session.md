# 쿠키와 세션

### 쿠키

<aside>
💡 웹 서버가 생성해 웹 브라우저로 전송하는 작은 정보 파일

</aside>

무상태인 HTTP 통신에서 클라이언트의 요청을 기억하고 구분하려는 용도로 사용

클라가 서버에 어떤 요청을 보냄 → 서버는 클라에 응답 시 쿠키 정보를 포함해 응답 → 클라는 응답받은 값에 쿠키가 있으면 자신의 기억 장치에 저장 → 요청을 보낼 때 저장했던 쿠키를 넣어 전송 → 서버는 요청에 포함된 쿠키 정보를 보고 클라이언트 식별 → 클라와 주고받은 과거 통신 내역에 대한 일부 데이터 저장

서버가 클라이언트로부터 요청을 받아 응답을 보낼 땐 Set-Cookie라는 헤더 정보 전송

```java
Set-Cookie: <쿠키_이름>:<쿠키_값>
```

```java
const app = require('express')();
app.get('/', (req, res) => {
	res.setHeader('Set-Cookie', [username='hihi']);
	res.sendFile(`${_dirname}/index.html`);
});
app.listen(8080, () => console.log('listening on port :8080'));
```

**쿠키 속성**: 어떤 요청을 보내고 받은 응답 헤더의 일부에 set-cookie 값으로 포함된 쿠키 정보들

- 쿠키 만료 시간 (expries, max-age)
    
    expires=Wed, 3 Sep 2023 09:00:00 GMT → 날짜 명시
    max-age=3600 → 기간 명시
    
- 쿠키 범위 (domain, path)
    
    domain=[example.com](http://example.com): example.com 도메인과 서브 도메인에서 접근 가능
    
    path=/mypage → mypage 경로와 그 하위 경로( ex: /mypage/profile )에서 접근 가능
    
- 쿠키 보안 (secure)
    
    민감한 정보를 쿠키로 전달해야할 때 secure 속성으로 지정 (HTTPS를 사용할 때만 전송)
    
- XSS 공격 방지 (HttpOnly)
    
    쿠키를 탈취하는 악성 공격 방법: XSS (사이트 간 스트립팅)
    
    → HttpOnly 속성을 사용해 클라가 쿠키에 접근하지 못하게 함
    
- CSRF 공격 방지 (samesite)
    
    해커가 쿠키를 악용하는 방법: CSRF (사이트 간 요청 위조)
    
    → samesite를 사용하는데 이의 속성인 strict, lax, none 중 하나를 지정
    
    - samesite의 속성
        
        strict: 다른 사이트로 쿠키 전송 가능
        
        lax: 안전한 http 메서드, 작업이 최상위 경로에서 이뤄지는 경우 제외하고 밖의 사이트로 쿠키 전송 불가
        
        none: 타 사이트로 쿠키 전송 가능 (이 옵션 사용하면 안됌)
        

### 세션

<aside>
💡 서버가 자신에게 요청을 보낸 클라이언트의 상태를 유지하기 위한 방법

</aside>

쿠키보다 보안관점 더 안전한 방법을 사용하고 싶을 때 세션 사용

클라가 서버에 어떤 요청을 보냄 → 서버는 무작위로 생성한 고유 세션 ID를 응답 메시지의 Set-Cookie 헤더 정보에 포함해 전달 → 클라는 요청 메시지를 보낼 때마다 응답받은 세션 ID 포함해 보냄 → 서버는 클라의 요청 메시지에 있는 세션 ID를 보고 유효한지 확인 후 요청 처리

> 웹브라우저와 같은 클라가 종료되면 즉시 삭제
새로운 클라이언트가 요청을 보내면 세션 ID를 주고받는 과정 처음부터 다시 수행
>
