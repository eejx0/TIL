# preconnect, preload, prefetch
<aside>
✏️

`<link>` 요소의 rel 속성값 `preconnect`, `preload`, `prefetch`

</aside>

→ 리소스(이미지, 폰트, css, js) 로드의 우선순위를 설정해 로드 성능을 최적화하기 위해 사용

- 리소스 과정
    
    브라우저가 네트워크 요청을 하고 응답을 기다린 후에야 리소스 사용 가능
    어떤 리소스는 미리 준비해두면 더 빠르게 화면을 그릴 수 있음 😮
    
    `preconnect`, `preload`, `prefetch`는 브라우저가 리소스를 더 효율적으로 가져오도록 도와주는 설정
    

### preconnect (미리 연결)

> **브라우저가 특정 origin에 대한 네트워크 연결을 미리 설정하도록 지시**
> 

🤖: 이 사이트에서 리소스 가져올 거니까 미리 연결해둬!

<aside>
💬

**웹사이트에서 구글 폰트를 가져오는 경우**

---

- 브라우저가 구글 서버와 연결을 맺고 리소스를 요청해야함
- 연결을 맺는 과정 (**DNS 조회, SSL 연결**) 시간이 걸림
- preconnect 사용 시 브라우저가 **미리 서버와 연결**을 맺어두고 **리소스를 더 빨리 가져올 수 있음**
    
    ```html
    <link rel="preconnect" href="https://fonts.googleapis.com">
    ```
    
</aside>

### preload (미리 로드)

> **특정 리소스를 미리 가져오도록 브라우저에 지시**
> 

🤖: 이 리소스는 반드시 필요하니까 미리 다운받아둬!

<aside>
💬

**CSS, JS, 이미지 같은 파일들을 HTML을 다 분석한 후에 요청하는 경우**

---

- 렌더링에 꼭 필요한 리소스라면 늦게 로드되면 안됌
- preload 사용 시 필수 리소스를 미리 로드할 수 있음
    
    ```html
    <link rel="preload" href="/styles.css" as="style">
    ```
    
</aside>

### prefetch (미리 가져오기)

> **브라우저가 향후 필요할 가능성이 있는 리소스를 미리 가져오도록 지시**
> 

🤖: 이 리소스는 나중에 쓸거니까 미리 받아둬!

<aside>
💬

**현재 페이지에서는 필요 없지만 다음 페이지에서 필요할 리소스인 경우**

---

- prefetch 사용 시 브라우저가 백그라운드에서 미리 다운로드해 다음에 해당 리소스를 사용할 때 훨씬 빠르게 로드 가능
    
    ```html
    <link rel="prefetch" href="/next-page.html">
    ```
    
</aside>
