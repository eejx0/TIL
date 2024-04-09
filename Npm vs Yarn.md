# npm vs yarn

## npm

> Node.js의 **기본 패키지 관리자** 🙂
> 

👉🏻 npm 툴을 이용해 Node 패키지를 만들고 업로드해 공유할 수 있음

npm **init**: **package.json** 생성

npm **install**: package.json 파일 및 해당 종속성에 나열된 **모든 모듈** 설치

npm **install package_name@버전**: 특정 패키지의 **특정 버전** 설치

npm **install 주소**: 특정 저장소 내 패키지 설치 (주로 github를 이렇게 설치)

npm **install package_name -g**: **글로벌**로 설치 → 로컬의 타 프로젝트도 이 패키지 사용 가능하게 됨

npm **uninstall**: 패키지 **삭제** 명령어

npm **update**: 설치한 패키지들 **업데이트**

npm **dedupe**: **중복** 설치된 패키지들 **정리**

## yarn

> npm과 같은 기능을 수행 but **속도나 안정성 측면**에서 npm보다 **향상** 😄
> 

**배경**❓

2016년 페이스북에서 개발한 패키지 관리자

→ 리액트와 같은 프로젝트를 진행하며 겪었던 어려움 해결

yarn **init**: package.json 생성

yarn or yarn install: package.json 파일 및 해당 종속성에 나열된 **모든 모듈** 설치

yarn **add package_name@버전**: 특정 패키지의 **특정 버전** 설치

yarn **add 주소**: 특정 저장소 내 패키지 설치 (주로 github를 이렇게 설치)

yarn global add package_name: **글로벌**로 설치 → 로컬의 타 프로젝트도 이 패키지 사용 가능하게 됨

yarn remove: 패키지 **삭제** 명령어

yarn upgrade: 설치한 패키지들 **업데이트**

npm **dedupe**: **중복** 설치된 패키지들 **정리**

## npm vs yarn

**속도**

> npm과 yarn의 주요 차이점 중 하나는 패키지 설치 프로세스를 처리하는 방법
> 

**npm**
패키지를 한 번에 하나씩 순차적으로 설치

**yarn**
여러 패키지를 동시에 가져오고 설치하도록 최적화되어 있음

**보안**

> yarn은 보안 측면에서 npm보다 더 안전
> 

**npm**
자동으로 패키지에 포함된 다른 패키지 코드를 실행

**yarn**
yarn.lock 또는 package.json 파일에 있는 파일만 설치
