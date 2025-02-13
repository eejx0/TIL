# Node와 Element의 차이
## Node

> **DOM을 구성**하는 가장 **기본적인 구성 단위**
> 

→ `Document Node`: HTML 문서 전체를 나타내는 루트 노드

→ `Element Node`: HTML 태그

→ `Text Node`: 텍스트 내용

→ `Comment Node`: 주석

## Element

> **Node의 특정 타입** 중 하나로 **HTML**이나 **XML 태그**로 표현되는 **객체**
> 

모든 Element는 Node이지만 모든 Node는 Element가 아니다

- id, class, styled 같은 HTML 속성을 가질 수 있음
- querySelector()나 getElementsByClassName() 같은 메서드 사용 가능

## 예시

`<div>Hello<!--주석—->World</div>`

- div 태그는 Element Node이면서 동시에 Node
- Hello, World 텍스트는 Text Node
- 주석은 Comment Node
- 모두 Node이지만 Element는 아님 🙌🏻
