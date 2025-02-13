# CORS, SOP
## SOP 🤔

> **웹 보안 정책** 중 하나로 **같은 출처에서만 요청을 허용**한다는 규칙
> 

→ 출처(origin): 프로토콜 + 도메인 + 포트 (ex: [https://example.com:443](https://example.com/))

- A 웹사이트에서 B 서버로 요청을 보낼 때 SOP가 적용되면 기본적으로 차단됌
- 악성 사이트가 사용자의 중요한 정보를 빼가거나 악용하는 것을 막음

## CORS 🤔

> Cross Origin Resource Sharing, 교차 출처 리소스 공유
> 

→ SOP의 예외를 허용하는 방법 (다른 출처에서도 허용해준다고 서버에서 허락하는거)

## CORS 설정 없이 SOP를 우회해 외부 서버와 통신할 수 있는 방법

### 프록시 서버 사용

> 브라우저 대신 **외부 서버에 요청**을 보내고 **응답을 받는 역할**을 **대리 수행하는 서버**
> 
- 브라우저가 직접 외부 서버에 요청하지 않고 클라와 동일한 origin의 프록시 서버로 요청을 보내면 SOP 제한 피하기 가능
- 클라이언트 측 도메인이 client.com, 서버 측 도메인이 server.com일 때 브라우저가 아닌 클라이언트 서버로 server.com에 요청을 보내면 응답을 받을 수 있게 됌 → 서버와 서버 간 통신엔 SOP가 적용되지 않음

### JSONP (JSON with Padding)

> script 태그로 json의 데이터를 가져오는 방식 (요즘엔 거의 안씀)
> 
- 서버에선 Access-Control-Allow-Origin 설정
- CORS 설정이지만 서버가 허용하면 해결됌
