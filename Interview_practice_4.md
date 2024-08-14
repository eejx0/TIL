## Sass

### 정의

> Syntactically Awesome Style Sheets
> 

<aside>
💡 CSS 전처리기 중 하나로 CSS를 더 효율적으로 작성할 수 있게 도와줌

</aside>

→ SCSS와 Sass 두 가지 구문 지원

→ SCSS는 CSS와 거의 동일한 문법을 사용하지만 Sass는 중괄호와 세미콜론 사용하지 않아도 됌

브라우저는 직접 Sass 파일을 이해하지 못함,,

CSS 전처리기로서 Sass 파일을 CSS 파일로 컴파일해 브라우저가 이해할 수 있는 CSS 파일로 변환해야 함

### 문법 & 구문

- $ 기호를 사용해 변수 정의 가능
    - ex) `color: $primary-color;`
- 선택자를 중첩하여 작성 가능
- @mixin을 사용해 스타일 블록을 정의하고 @include를 사용해 해당 스타일 블록 적용
    - 스타일 재사용, 코드 간결하게 작성
- @extend를 사용해 스타일 상속 가능
    
    ```css
    .btn {
      display: inline-block;
      padding: 8px 16px;
      font-size: 14px;
      color: #fff;
      text-align: center;
      background-color: #0275d8;
      border-radius: 4px;
    }
    
    .btn-primary {
      @extend .btn;
      background-color: #5cb85c;
    }
    ```
    

## cubic bezier

### 정의

> transition → timing-function → cubic-bezier
> 

ex) 예시 코드

```css
.Wrapper {
	transition: 0.5s;
	transition-timing-function: cubic-bezier(0.075, 0.82, 0.165, 1);
}
```

### 베지어 곡선

> 곡선을 매끄럽게 잘 그릴 수 있게끔 해주는 곡선 알고리즘
> 
- 1차 베이지 곡선: linear-bezier-curve
- 2차 베이지 곡선: quadratic-bezier-curve
- 3차 베이지 곡선: cubic-bezier-curve

## 시맨틱 태그의 의미와 종류

### 의미

<aside>
💡 의미가 있는 태그 (Semantic: 의미의, 의미론적인)

</aside>

### 종류

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/ed08f4e9-4934-479f-a55b-09ffbf96beb6/f0e47daa-1f5f-4b83-897e-3a22e90b796f/image.png)

- header
- nav
- main
- footer
- aside
- section
- ins
- u
- blockquote
- q
- figcaption

- article
- details
- mark
- time
- address
- b
- cite
- dfn
- code
- a
- kbd

- strong
- em
- i
- small
- del
- s
- sup
- sub
- wbr
- figure

### 장점

1. 검색 엔진 최적화
    
    > 태그를 기반으로 페이지 내 검색 키워드의 우선순위 판단
    > 
    > 
    > 따라서 의미에 맞는 올바른 태그를 사용하는 것이 중요
    > 
2. 시각장애인분들이 스크린 리더를 사용해 페이지 탐색 시 도움이 됨
    
    스크린 리더: 시각 장애인이 눈으로 보는 대신 소리로 들려주면서 정보 전달
    
3. 시멘틱 태그를 사용한 코드 블록을 찾는 것은 div를 탐색하는 것보다 훨씬 쉬움

## 시맨틱 태그와 div의 차이

## Meta 태그의 쓰임새

### 정의

> <meta> 태그는 해당 문서에 대한 정보인 메타데이터를 정의할 때 사용
하이퍼텍스트 생성 언어 HTML 문서의 맨 위쪽에 위치
> 
- head 태그 사이 또는 뒤에 있어도 되지만 반드시 body 태그 앞쪽에 위치해야 함
- 웹페이지의 요약이므로 상당이 중요!
- 검색 엔진 최적화에도 영향을 미치며 웹페이지가 보여지는 방식을 결정할 수 있음

### 속성

- http-equiv (웹 브라우저 서버에 명령을 내림)
- content (meta 정보의 내용을 지정)
- name (몇 개의 meta 정보의 이름을 정할 수 있으며 지정하지 않으면 http-equiv와 같은 기능)

### 사용하는 이유

<aside>
💡 html을 통해 만든 웹페이지를 보다 브라우저가 개괄적으로 판단할 수 있게 하기 위해서

</aside>

### 줌인 줌아웃 조절 속성

- user-scalable → no로 설정하면 사용자가 줌인/줌아웃 할 수 없게 됌
- 최소 최대 비율 설정 → mininum-scale, maximum-scale
