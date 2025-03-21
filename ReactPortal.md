# 리액트 포탈
### 🗣 React Portal

---

> **부모 컴포넌트의 DOM 계층 구조 바깥에 있는 DOM 노드로 자식을 렌더링하는 최고의 방법을 제공**
> 

리액트는 부모 컴포넌트가 렌더링되면 자식 컴포넌트가 렌더링되는 `tree 구조`를 갖고 있음
이런 `tree 구조`는 부모-자식 관계를 갖게되는데 DOM 계층 구조에 영향을 미침

→ **리액트 포탈**을 사용하면 **독립적인 위치에서 렌더링**하기 때문에 **편리하게 사용** 가능

- 스타일링이 간편
- 독립적인 위치에서 렌더링을 하면 z-index 같은 속성을 부모 컴포넌트에 영향을 받지 않고 사용 가능
- 유지보수성 향상, CSS 충돌 방지

### 🗣 사용 방법

<aside>
📎

**index.html**

---

```html
<!DOCTYPE html>
...
<body>
	<div id="root"></div>
	<aside id="aside-root"></aside> <!-- React Portal을 위한 코드 -->
</body>
```

- React는 기본적으로 #root 안에 렌더링 되지만 포탈 사용 시 다른 DOM 요소로 렌더링 가능
- aside 코드가 포탈을 위한 대상 DOM 요소가 됌
</aside>

<aside>
📎

**Home.tsx**

---

```tsx
import { createPortal } from 'react-dom';

const Modal = () => {
  return createPortal(
    <div className="modal">모달 내용</div>,  // 렌더링할 JSX
    document.getElementById('aside-root')  // 포탈 대상 DOM 요소
  );
};
```

- createPortal은 첫 번째 인자로 렌더링할 JSX 요소, 두번째 인자로 포탈 대상 DOM 요소를 받음세번째 파라미터는 옵션인데 포털의 키로 사용할 고유 문자와 숫자 key 값을 나타냄
- 예시대로 하면 #aside-root 요소에 렌더링할 JSX 부분을 렌더링하고 있는거임
</aside>

### 🗣 특징

---

**Portal로 컴포넌트를 설정한 DOM element로 텔레포트**

- Portal를 이용해 모달의 DOM을 다른 위치로 텔레포트 시킬 수 있음 (다른 위치로 렌더링 가능)
- 리액트 포탈을 이용한 자식 컴포넌트는 부모 컴포넌트 트리가 제공하는 컨텍스트에 접근이 가능하고 이벤트는 여전히 React tree에 따라 자식에서 부모로 버블링 됌

![image.png](attachment:b2834dd0-9870-4c04-80b8-45c379f4a145:image.png)

- 원래 ReactPortal 태그 코드는 Home.tsx에 위치해야했음
- 텔레포트 시켜서 DOM element인 aside-root로 이동

**Portal에 렌더링된 컴포넌트는 DOM에서 부모 JSX 요소에 포함되지 않음**
