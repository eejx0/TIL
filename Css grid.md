# CSS Grid
### flex와 Grid의 차이

> **Flex**는 **한 방향** 레이아웃 시스템
**Grid**는 **두 방향** (가로 세로) 레이아웃 시스템
> 

### 용어 정리

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/ed08f4e9-4934-479f-a55b-09ffbf96beb6/ce992ae4-2f2f-4334-93c9-79af9f67c8f5/Untitled.png)

- 그리드 컨테이너
    - display: grid를 적용하는 Grid의 전체 영역
    - Grid 컨테이너 안의 요소들이 Grid 규칙의 영향을 받아 정렬됌
- 그리드 아이템
    - Grid 컨테이너의 자식 요소들
    - 이 아이템들이 Grid 규칙에 의해 배치됌
- 그리드 트랙
    - Grid의 행 또는 열
- 그리드 셀
    - Grid의 한 칸을 가리킴
    - div 같은 실제 html 요소는 그리드 아이템, 이런 Grid 아이템 하나가 들어가는 가상의 칸
- 그리드 라인
    - Grid 셀을 구분하는 선
- 그리드 번호
    - Grid 라인의 각 번호
- 그리드 갭
    - Grid 셀 사이의 간격
- 그리드 영역
    - Grid 라인으로 둘러싸인 사각형 영역
    - 그리드 셀의 집합

### 그리드 형태 정의

```css
.Wrapper {
	grid-template-columns: 200px 200px 500px;
	/* grid-template-columns: 1fr 1fr 1fr */
	/* grid-template-columns: repeat(3, 1fr) */
	/* grid-template-columns: 200px 1fr */
	/* grid-template-columns: 100px 200px auto */
	
	/* row도 동일 */
}
```

grid-template-row는 행 배치

grid-template-columns는 열 배치

ex) `grid-template-columns: 200px 200px 500px`

→ column을 200px, 200px, 500px로 만들겠다는 의미

ex) `grid-template-columns: 1fr 1fr 1fr`

→ fr은 fraction으로 숫자 비율대로 트랙의 크기를 나눔

→ 즉 위의 1fr 1fr 1fr은 균일하게 1:1:1 비율인 3개의 column을 만들겠다는 의미

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/ed08f4e9-4934-479f-a55b-09ffbf96beb6/a49c34f7-2e06-4642-82bf-10d3b9d3c403/Untitled.png)

ex) `grid-template-columns: 100px 2fr 1fr`

→ 첫번째 column은 100px로 고정되고 나머지 두번째 세번째 column은 2:1 비율로 움직임

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/ed08f4e9-4934-479f-a55b-09ffbf96beb6/598ce96b-f0e3-4b09-8d3e-5db612e22978/Untitled.png)

**repeat 함수**

`grid-template-column: repeat(5, 1fr)` === `grid-template-columns: 1fr 1fr 1fr 1fr 1fr`

→ 이처럼 반복되는 값을 자동으로 처리할 수 있는 함수임

→ repeat(반복횟수, 반복값) repeat(3, 1fr 4fr 2fr)도 가능

**minmax 함수**

ex) 

```css
.Wrapper {
	grid-template-columns: repeat (3, 1fr);
	grid-template-rows: repeat (3, minmax(100px, auto));
}
```

→ 최소한 100px, 최대는 자동으로 늘어나게

→ 아무리 내용의 양이 적더라도 최소한 높이 100px은 확보

→ 내용이 많아 100px이 넘어가면 알아서 늘어나도록 처리해줌

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/ed08f4e9-4934-479f-a55b-09ffbf96beb6/0a89dc3e-bd0a-40e3-866b-f91529dcc991/Untitled.png)

**auto-fill & auto-fit**

ex) `grid-template-columns: repeat(auto-fill, minmax(20%, auto))`

→ auto-fill의 크기를 20%로 설정했으므로 1개의 row엔 5개의 셀이 들어감

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/ed08f4e9-4934-479f-a55b-09ffbf96beb6/f8ec93e6-cede-4aca-9083-617ce137d3f6/Untitled.png)

→ auto-fit으로 하면 맨 밑에 남은 공간을 채움

### 간격 만들기

```css
.Wrapper {
	row-gap: 10px;
	column-gap: 20px;
	/* gap: 10px 20px */
}
```

### 그리드 형태 자동으로 정의

`grid-auto-rows: minmax(100px, auto);`

→ 횟수를 지정해서 반복할 필요 없이 알아서 처리됌

### 각 셀의 영역 지정

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/ed08f4e9-4934-479f-a55b-09ffbf96beb6/db4c42f9-08c6-4956-a8fd-2a44d744a545/Untitled.png)

→ 번호를 이용해 column과 row의 범위 결정

→ grid-column-start: 시작 번호, grid-column-end: 끝 번호, grid-column: start와 end 축약형

```css
.item: nth-child(1) {
	grid-column-start: 1;
	grid-column-end: 3;
	grid-row-start: 1;
	grid-row-end: 2;
}
```

```css
.item: nth-child(1) {
	grid-column: 1 / 3;
	grid-row: 1 / 2;
}
```

```css
.item: nth-child(1) {
	/* 1번 라인에서 2칸 */
	grid-column: 1 / span 2;
	/* 1번 라인에서 3칸 */
	grid-row: 1 / span 3;
}
```

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/ed08f4e9-4934-479f-a55b-09ffbf96beb6/c51276ce-dbce-456d-8bf1-4ad65ad152b5/Untitled.png)

### 영역 이름으로 그리드 정의

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/ed08f4e9-4934-479f-a55b-09ffbf96beb6/141c9244-003a-49ab-a43b-51d76d789eee/Untitled.png)

→ 각 영역에 이름을 붙이고 그 이름을 이용해서 배치하는 방법

```css
.Wrapper {
	grid-template-areas:
		"header header header"
		"a main a"
		". . ."
		/* 빈칸은 마침표 또는 none을 사용하면 됌 */
		"footer footer footer";
}
```

```css
.header { grid-area: header; }
.sidebar { grid-area: a; }
.main { grid-area: main; }
.
.
.
```

→ 각 영역의 이름은 해당 아이템 요소에 grid-area 속성으로 이름을 지정해주면 됌

### 세로 방향 정렬

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/ed08f4e9-4934-479f-a55b-09ffbf96beb6/6088b8d1-5645-489d-b097-a843469bc113/Untitled.png)

`align-items: stretch` 일 때

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/ed08f4e9-4934-479f-a55b-09ffbf96beb6/b748b9cb-26c4-4fb4-a17a-1b8fb7c8f165/Untitled.png)

`align-items: center`일 때

### place-items

- align-items와 justify-items를 같이 쓸 수 있는 단축 속성
- align-items, justify-items의 순서로 작성하고 하나의 값만 쓰면 두 속성 모두에 적용됌
- `place-items: center start;`
