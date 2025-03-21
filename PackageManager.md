# 패키지 매니저
## pnpm

> **npm에 비해 성능과 디스크 효율성을 개선한 패키지 매니저**
> 

<aside>
🗣

**특징**

---

- `content-addressable store`라는 전역 저장소에 패키지 보관 후
- 패키지를 한 곳(전역 저장소)에만 저장하고 각 프로젝트에선 실제 파일이 아니라 링크만 걸어둠
- **동일한 패키지를 여러 프로젝트에서 공유** 가능
</aside>

- 설명
    
    **만약 a라는 프로젝트에서 npm이나 yarn으로 axios를 설치했다고 해보자** 🤔
    
    `npm, yarn`: node_modules의 a라는 프로젝트 폴더 안에서 axios 패키지의 복사본이 저장
    
    `pnpm`: 전역 저장소에 axios 패키지가 저장되어있기 때문에 실제 파일이 아닌 전역 저장소를 가리키는 링크가 저장되어 있음
    
    **여기서 b라는 프로젝트에도 똑같은 방법으로 axios를 설치하면** 🔥
    
    `npm, yarn`: b라는 프로젝트 폴더 안에서 또 axios 패키지의 복사본이 저장.. → 용량 낭비
    

## Yarn Berry

> **PnP(Plug’n’Play), Zero Install을 도입해 패키지 관리 방식을 개선한 패키지 매니저**
> 

→ Yarn의 2.0 버전 이상

<aside>
🗣

**특징**

---

- node_modules 폴더를 없애고 `.pnp.cjs` 파일을 이용해 **의존성 관리**
- .pnp.cjs엔 패키지 위치와 의존성 정보들이 완전히 기술되어있어 패키지를 찾는 과정이 효율, 정확
- .yarn/cache 디렉토리에 패키지들이 zip 압축 파일 형태로 관리되어 용량 ⬇️
- 의존성들을 버전 관리에 포함시켜 git으로 관리 가능
</aside>

## 공통점

- 설치 속도 ⬆️
- 스토리지 용량 ⬇️
- 유령 의존성 문제 ❌
- workspace 기능으로 모노레포를 구성하는 데 활용 가능

### 유령 의존성 문제란 👻

> Ghost Dependency
> 

A 패키지가 B 패키지에 의존하고 있다치자, 그런데 내 프로젝트에서 B를 직접 설치하지 않은거지

`yarn add A` 라는 명령어로 A만 설치했는데 A가 B를 필요로 하니까 node_modules 폴더 안에는 B도 자동으로 깔려 있음..

1. B를 직접 설치한 적이 없어서 package.json에는 B가 없음
2. node_modules에는 B가 깔려있음
3. 나중에 A가 B에 대한 의존성을 없애거나 버전을 바꾸면
    
    → node_modules에 있던 B가 사라져서 코드가 갑자기 깨질 수 있음
    
    → 갑자기 실행이 안되는 문제 발생 🙀
