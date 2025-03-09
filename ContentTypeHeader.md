# Content-Type 헤더
> **HTTP 요청과 응답에서 전송되는 데이터의 타입을 명시하는 헤더**
> 

→ 서버와 클라이언트가 데이터를 주고받을 때 제대로 해석할 수 있도록 하기 위해 사용

<aside>
✅

**JSON 데이터를 전송하는 경우 (예시)**

---

- `Content-Type: application/json` 사용
- 서버는 해당 데이터가 JSON 형식이라는걸 알고 적절히 해석
- 아니면 서버가 클라이언트에게 HTML을 응답할 때 `Content-Type: text/html`을 지정해 브라우저가 HTML로 렌더링 가능
- Content-Type 헤더는 MIME 타입을 기반으로 해 **`[type]/[subtype]`** 형식으로 구성
</aside>

### Accept 헤더와의 차이 🤔

> **Content-Type** 헤더는 **전송되는 데이터 타입** 지정
**Accept** 헤더는 **응답으로 받고자하는 데이터 타입** 지정
> 

클라이언트가 JSON 응답을 원할 경우 → `Accept: application/json`
