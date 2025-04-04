# Cache-Control 헤더
> **클라이언트와 중간 서버(proxy, CDN 등)가 어떤 방식으로 캐싱할지를 지정하는 헤더**
> 

특정 응답을 얼마나 오래, 어떻게 캐싱할 것인가 → 불필요한 네트워크 요청을 줄이고 웹 성능 개선 가능

**특정 리소스를 얼마나 오래 저장할 수 있는지를 서버가 결정하는 것** ✅

---

- 웹 페이지를 방문할 때 브라우저는 서버에서 `html`, `css`, `js` 등의 리소스를 다운로드
- 이 리소스를 매번 다시 다운로드하지 않고 저장된 데이터를 활용하면 성능이 향상될 수 있음
- 모든 리소스를 무조건 캐시에 저장하면 최신 데이터가 반영되지 않을 수 있어 리소스 유형 별로 적절한 캐싱 정책을 설정하는 것이 중요

### 디렉티브

<aside>
🗣

**no-store**

---

- 캐싱을 하지 않겠다는 뜻
- 헤당 헤더를 브라우저가 응답 받을 경우 response를 캐싱하지 않음
- SPA에서 라우팅 변경이나 `뒤로가기/앞으로가기`로 다시 요청이 필요할 경우엔 무조건 다시 요청
(SPA: Single Page Application)
</aside>

<aside>
🗣

**no-cache**

---

- 캐싱을 하지만 변경 되었는지 확인하겠다는 뜻
- 서버에서 200 응답이 오면 해당 응답을 사용하지만 304가 오면 캐싱했던 응답을 재사용
- 매번 요청을 보내야 되긴 하지만 변경되지 않았을 경우엔 캐싱된 응답을 사용하면 되기 때문에 빠르고 사이즈가 작은 응답을 받을 수 있음
</aside>

<aside>
🗣

**max-age=<seconds>**

---

- 응답을 받은 뒤 지정한 시간동안에만 캐싱된 응답을 재사용하고 지정된 시간이 지나면 서버로 다시 요청
- 304 응답을 받으면 캐싱된 응답의 캐싱시간을 지정한 시간만큼 연장
- max-age=0은 no-cache와 같음
</aside>

### 캐싱의 장점

- 사용자의 대역폭 소비 줄임
- 서버 부하 낮춤
- 페이지 로딩 속도 개선
- 네트워크 환경이 열악한 모바일에서 캐싱이 더욱 중요한 역할을 함
