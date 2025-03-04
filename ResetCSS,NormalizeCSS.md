# Reset CSS, Normalize CSS
> **브라우저 간의 스타일 차이**를 줄이기 위해 사용되는 **CSS 파일**
> 

### Reset CSS

<aside>
💡

**모든 브라우저의 기본 스타일을 완전히 제거** ✅

---

- ex: html 요소에 기본으로 적용된 패딩, 글자 크기 등을 초기화
- 특정 브라우저의 기본 스타일에 영향을 받지 않고 스타일링 시작 가능
- 스타일을 처음부터 새롭게 작성해야하지만 완전한 스타일 통일성 보장
</aside>

```css
* {
  margin: 0;
  padding: 0;
  border: 0;
  font-size: 100%;
  font: inherit;
  vertical-align: baseline;
}
```

### Normalize CSS

<aside>
💡

**브라우저 간 스타일 차이를 줄이는데 중점** ✅

---

- 브라우저 간 일관되지 않은 스타일만 수정해 자연스러운 기본값 유지
- ex: 제목 태그의 기본 크기나 폰트를 브라우저마다 일관되게 조정하며 요소의 기본 스타일은 둠
- 자연스러운 초기 스타일 유지
- 브라우저 간의 주요한 차이만 해소
</aside>

```css
h1 {
  font-size: 2em;
  margin: 0.67em 0;
}
a {
  background-color: transparent;
}
```

### 어떤 방식이 더 좋을까

데드라인이 빠르고 일일이 스타일링 하기 힘들때 → **Normalize CSS** 선택

디자인 시스템처럼 직접 스타일링이 중요하다 → **Reset CSS** 선택
