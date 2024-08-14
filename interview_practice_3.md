## CSS 속성

- CSS 선택자
- CSS Colors
- CSS 배경
- CSS 테두리
- CSS 여백과 패딩
- CSS 텍스트
- CSS 링크
- CSS 플로트

## Styled-component

> **Styled-component** (CSS-in-JS의 라이브러리)
> 

### **CSS in JS**

- 스타일 정의를 css나 scss 파일이 아닌 js로 작성된 컴포넌트에 바로 삽입하는 스타일 기법
- import 해서 활용

### CSS in JS의 장점

- css의 컴파일화로 스타일시트의 파일을 유지보수 할 필요 x
- js 환경 최대 활용 가능
- js와 css 사이의 상수와 함수 쉽게 공유 가능 (React에선 props를 활용한 조건부 스타일링 가능)
- 현재 사용중인 스타일만 dom에 포함
- 짧은 길이의 유니크한 클래스 자동 생성 → 코드 경량화

### CSS in JS의 단점

- 학습 곡선이 커짐
- 별도의 라이브러리 설치 → 번들 크기 커짐
- 인터랙션한 페이지일 경우 css 파일 따로 관리하는 방법에 비해 느린 성능을 보일 수 있음

## CSS position 종류

- static (기본 값)
    - 포지션을 설정하지 않았을 때 기본적으로 설정되는 값
    - left, right, top, bottm의 영향 x, 화면의 흐름대로 나열
- relative
    - 요소를 원래 위치에서 벗어나게 배치
    - 원래 위치의 공간은 차지하지만 top, right, bottm, left에 따라 상대적인 위치로 이동
- absolute
    - 배치 기준을 자신의 상위 요소에서 찾음
    - position 속성이 static이 아닌 속성을 가진 요소 중 가장 가까운 요소 기준으로 배치
    - 만약 없다면, body가 배치의 기준이 됨
    - 원래 위치의 공간 차지 x
- fixed
    - 화면을 스크롤해도 고정되는 내비게이션 처럼 부모요소가 아닌 뷰포트를 기준으로 고정된 위치에 배치
- sticky
    - 원래 위치에 있다가 화면 스크롤 시 화면에 따라 움직임

## CSS 초기화의 필요성

### reset CSS

> 웹 브라우저마다 default 값으로 스타일이 알아서 적용됨
> 

```css
html, body, div, span, applet, object, iframe,
h1, h2, h3, h4, h5, h6, p, blockquote, pre,
a, abbr, acronym, address, big, cite, code,
del, dfn, em, img, ins, kbd, q, s, samp,
small, strike, strong, sub, sup, tt, var,
b, u, i, center,
dl, dt, dd, ol, ul, li,
fieldset, form, label, legend,
table, caption, tbody, tfoot, thead, tr, th, td,
article, aside, canvas, details, embed, 
figure, figcaption, footer, header, hgroup, 
menu, nav, output, ruby, section, summary,
time, mark, audio, video {
	margin: 0;
	padding: 0;
	border: 0;
	font-size: 100%;
	font: inherit;
	vertical-align: baseline;
}
/* HTML5 display-role reset for older browsers */
article, aside, details, figcaption, figure, 
footer, header, hgroup, menu, nav, section {
	display: block;
}
body {
	line-height: 1;
}
ol, ul {
	list-style: none;
}
blockquote, q {
	quotes: none;
}
blockquote:before, blockquote:after,
q:before, q:after {
	content: '';
	content: none;
}
table {
	border-collapse: collapse;
	border-spacing: 0;
}
```
