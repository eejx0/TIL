# Vite
<aside>
💡 ‘**빠르다**’는 의미
간결한 모던 웹 프로젝트 개발 경험에 초점을 맞춰 탄생한 빌드 도구

</aside>

### 등장 이유

프로젝트 규모가 커지며 webpack, Rollup같은 **번들링 도구들이 필요**해짐

→ 개발 경험을 크게 향상 시킴

→ 프로젝트 수준이 더 높아지며 처리해야하는 js양도 기하급수적으로 증가

→ 개발 **서버를 시작하는데 많은 시간**이 소요되는 문제 발생!

- ES build를 사용해 종속성을 미리 묶음
    - 기존의 js 기반의 번들러보다 10~100배 더 빠른 속도로 종속성을 사전 번들링
        
        ![진짜 빠름](https://prod-files-secure.s3.us-west-2.amazonaws.com/ed08f4e9-4934-479f-a55b-09ffbf96beb6/41c3799c-afe8-4463-b34b-8d83edec8500/Untitled.png)
        
        진짜 빠름
        
- HMR(Hot Module Replacement) 사용
    - HMR 이용 시 애플리케이션을 다시 시작하지 않고도 일부 컨텐츠만 갱신
- 수정된 모듈만 교체
    - 어떤 모듈이 수정되면 vite는 그저 수정된 모듈과 관련된 부분만 교체
    - 브라우저에서 해당 모듈을 요청하면 교체된 모듈을 전달
- 캐시 기능 제공
    - HTTP 헤더를 활용해 전체 페이지의 로드 속도 높임
    - 요청 횟수를 최소화하여 페이지 로딩을 빠르게 만들어줌

### 작업 방식

> 모듈을 dependencies와 source code 두 가지로 나누어 개발 서버의 시작 시간 개선
> 

Dependencies

: 개발 시 그 내용이 바뀌지 않을 일반적인 js 소스 코드

기존 번들러로는 몇 백 개의 js 모듈을 갖고 있는 매우 큰 디펜던시에 대한 번들링 과정이 매우 비효율적이었고 많은 시간이 필요했음

⇒ Vite는 사전 번들링 기능은 Esbuild를 사용해 시간을 줄임

Source code

: JSX, CSS 또는 Vue/Svelte 컴포넌트와 같이 컴파일링이 필요하고 수정 또한 잦은 Non-plain JavaScript 소스 코드는 다르게 처리

Vite는 Native ESM을 이용해 소스 코드 제공

![기존](https://prod-files-secure.s3.us-west-2.amazonaws.com/ed08f4e9-4934-479f-a55b-09ffbf96beb6/fe8de502-4f37-4175-9ebc-64a1bc4c94f4/Untitled.png)

기존

![native esm](https://prod-files-secure.s3.us-west-2.amazonaws.com/ed08f4e9-4934-479f-a55b-09ffbf96beb6/bd6e2966-31bb-4081-a404-d833aea5331c/Untitled.png)

native esm

### 정리 (Vite는..)

1. 빠른 빌드
2. 라이브러리 설치 직후 미리 bundle을 만들어 놓음
3. 소스코드 변경 시 필요한 것만 수정
