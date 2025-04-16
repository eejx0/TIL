# px, em, rem
> 반응형같이 **유연한 페이지**를 디자인하고자 할 때 **em, rem 단위** 사용
> 

→ px는 값이 고정되어 있는 절대값의 단위이고 em, rem은 환경에 따라 변하는 상대 단위

**상대단위**: 고정되지 않고 어떤 기준에 따라 유동적으로 바뀌는 길이를 나타내는 단위

**절대단위**: 어떤 상황에서든 항상 고정된 길이를 나타내는 단위

### px

> **절대값을 사용하는 단위**
> 

<aside>
🗣

**문제점**

---

- 모든 브라우저는 사용자가 font-size 설정이 가능함
- 따로 font-size를 지정하지 않은 경우 16px로 표시되는데 개발자가 px로 고정하면
사용자가 브라우저 설정에서 font-size 변경을 하지 못함
</aside>

### em

> 해당 단위가 사용되고 있는 요소의 font-size를 기준으로 px로 바껴 화면에 표시됨
> 

→ 같은 엘리먼트에 설정된 폰트 크기 값이 없을 경우 상위 요소의 폰트 사이즈가 기준

```tsx
const Style = styled.div`
	font-size: 16px;
	padding: 1em;
`;
```

### rem

> r은 root 즉 최상위 엘리먼트에서 지정된 font-size의 값을 기준으로 변환
> 

```css
html {
	font-size: 16px;
}

div {
	font-size: 20px;
	width: 10rem;
}
```
