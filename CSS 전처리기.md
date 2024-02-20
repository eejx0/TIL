## CSS 전처리기

<aside>
💡 CSS 코드 자체의 재사용성을 증가시킬 수는 있어도 유지 보수나 관리의 용이성을 증가시키기엔 한계가 있어 개선을 위해 도입

</aside>

**CSS 전처리기 언어**: SCSS. LESS, Stylus …

**SCSS**

> CSS의 불편한 점을 개선하고 개발자에게 더 나은 스타일 시트를 작성하는 경험 제공
> 

```css
$font-size: 16px;

div {
	font-size: $font-size;
}
```

```css
@import "_form";
@import "_button";
```

```css
.card {
	border: 1px solid gray;
	.card-header {
		padding: 8px
	}
}
```

```css
.btn {
	width: 100px;
}
.btn-danger {
	@extend .btn; /* btn 선택자에 적용된 스타일 모두 가져오기 */
}
```

```css
@mixin bordered() { /* bordered()라는 스타일 정의 */
	border: 1px solid #ddd;
}
h1 {
	@include bordered(); /* bordered() 스타일 사용 */
}
```

```css
@mixin bordered($width: 5px) { /* bordered() 스타일 정의, 매개변수 사용 */
	border: 1px solid #ddd;
}
h1 {
	@include bordered(3px); /* bordered() 스타일 사용, 매개변수 값 변경 */
}
```

```css
$default: 10px;
div {
	height: ($default + 10); /* height: 20px */
}
```

```css
$theme: "darkmode";
body {
	@if ($theme == "darkmode") {
		color: white;
	} @else {
		color: black;
	}
}
```

```css
@for $i from 1 through 5 {
	.mt#{$i} {
		margin-top: $i + px;
	}
}
```

```css
.mt1 {
	margin-top: 1px;
}
.mt2 {
	margint-top: 2px;
}
```

**LESS**

> 개발자의 생산성을 높이기 윟 scss보다 더 간결하고 편리한 기능 추가
> 

```css
@font-size: 16px;
div {
	font-size: @font-size;
}
```

파일 가져오기, 충첩 문법은 SCSS와 동일

```css
.btn {
	width: 100px
}
.btn-danger {
	.btn;
	background-color: red;
}
```

```css
@base-color: #336699;
.lighter-color {
	background-color: lighten(@base-color, 20%); /* 20% 더 밝게 조정 */
}
```

```css
@condition: false;
.selector {
	color: if(@condition, red, blue); /* @condition이 true이면 red, false이면 blue */
}
```

```css
.generate-margins(@index) when (@index < 6) {
	.mt@{index} {
		margin-top: @index * 1px;
	}
	.generate-margins(@index + 1);
}

.generate-margins(1);
```
