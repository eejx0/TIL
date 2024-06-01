# Selection Object

### Selection

> window.getSelection()을 했을 때 얻을 수 있는 값이 Selection 객체
> 

→ Selection 객체는 **현재 커서의 위치**나 **선택한 범위**

### 속성 & 메소드

- Selection.anchorNode: 선택이 시작되는 위치
- Selection.anchorOffset: anchor의 Offset
    
    → anchorNode가 텍스트면 anchorNode 앞에 있는 문자 수를 나타냄
    
    → anchorNode가 요소면 anchorNode의 자식 노드 수를 나타냄
    
- Selection.focusNode: 선택이 끝나는 위치
- Selection.focuseOffset: focus의 Offset
    
    → anchorOffset의 focus 버전
    
- Selection.isCollased: 시작 지점과 끝 지점이 같으면 true, 다르면 false
- Selection.type: 범위를 지정하면 “Range”, 지정 안하면 “Caret”, 클릭을 안했다면 “None”
    
    → 새로 고침 후 클릭 하지 않은 상태에서 isCollapsed는 true, type은 none
    
- window.getSelection().collapse(dom, number): 커서를 dom의 number로 이동
