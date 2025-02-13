## transform

> **애니메이션**이나 **동적인 위치 변경**이 필요한 경우 선호
> 
- 브라우저의 composite 단계에서 실행
    
    composite 단계: 렌더링 과정에서 이전에 생성된 레이아웃 결과물을 화면에 그려줌
    
- reflow나 repaint를 유발하지 않음 (성능 상 이점)

## position

> **레이아웃의 구조**를 잡거나 **부모를 기준**으로 **위치를 조정**할 경우 선호
> 
- reflow나 repaint 유발
- 브라우저가 주변 요소들의 위치를 다시 계산하는 과정부터 다시 수행

```jsx
// transform
const Button = styled.button`
	&:hover {
		transform: translateY(-5px);
	}
`;

// position
const Button = styled.button`
	position: relative;
	&:hover {
		top: -5px;
	}
`;
```
