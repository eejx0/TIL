# hover

## hover란?

 hover css 클래스는 사용자가 포인팅 장치를 사용해 상호작용 중인 요소를 뜻함

→ 사용자의 커서가 요소에 올라가 있을 때 적용됨

```html
<a href = "#">이 링크를 가리켜 보세요.</a>
```

```css
a {
	background-color: powderblue;
	transition: background-color .5s;
}

a:hover{
	background-color: gold;
}
```