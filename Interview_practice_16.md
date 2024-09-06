action, store 등에 대한 개념을 다양한 관점에서 정리

## Flux 패턴

**등장 배경**

> 대규모 애플리케이션에서 **데이터 흐름**을 **일관성있게 관리**함으로써 **예측 가능성을 높이기** 위함
> 

기존엔 MVC 패턴 사용..

→ 문제점 등장

- Model에 데이터 저장하고 Controller를 이용해 Model의 데이터 관리
- 애플리케이션의 규모가 커지면 복잡한 데이터 흐름을 가지게 됌

![요랬는데..](https://prod-files-secure.s3.us-west-2.amazonaws.com/ed08f4e9-4934-479f-a55b-09ffbf96beb6/93a90caf-0f8e-4acf-a6db-20d1a203b9a2/image.png)

요랬는데..

![요렇게 되버림](https://prod-files-secure.s3.us-west-2.amazonaws.com/ed08f4e9-4934-479f-a55b-09ffbf96beb6/ff85a40a-0bba-4e44-9035-e4bf7ec9e25b/image.png)

요렇게 되버림

**flux 패턴?**

> **사용자 입력을 기반**으로 **action**을 만들고 action을 **dispatcher에 전달**해 
**store의 데이터를 변경**한 후 view에 반영하는 **단방향 흐름**으로 애플리케이션을 만드는 **아키텍처**
> 

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/ed08f4e9-4934-479f-a55b-09ffbf96beb6/0fa1f828-661a-4fae-a846-baed4bf101d2/image.png)

- action: 데이터를 변경하는 행위로서 dispatcher에게 전달되는 객체
- action creator: 새로 발생한 action의 타입과 새로운 데이터를 묶어 dispatcher에게 전달
    
    ```jsx
    {
    	type: 'SET_PROFILE'
    	data: {
    		'name': 'Harry',
    		'age': '11'
    	}
    }
    ```
    
- dispatcher: 모든 데이터의 흐름을 관리하는 중앙 허브
- store(model): 상태 저장소로서 상태와 상태를 변경할 수 있는 메서드를 가짐
- view: 리액트 컴포넌트
- action → dispatcher → model → view → action → dispatcher … (순환구조)

## Redux

### 정의

<aside>
🔨

**JavaScript 상태관리 라이브러리**

</aside>

→ Redux의 본질은 Node.js

→ **컴포넌트와 상태를 분리하는 패턴**을 써서 **상태 관리를 편하게** 도와주는 도구

→ **flux 패턴**에서 영감을 받아 **더 단순화하고 구조화된 형태**로 발전

- 복잡성 줄임
- 단일 store과 reducer 개념 도입
- 상태관리를 더 단순화하고 디버깅과 유지보수 더 쉽게 만듦

### 세 가지 원칙

**Single source of truth**

- 동일한 데이터는 항상 같은 곳에서 가지고 옴
- 스토어라는 하나뿐인 데이터 공간이 있다는 의미

*스토어: 상태가 관리되는 오직 하나의 공간

**State is read-only**

- 리액트에선 setState 메소드를 활용해야만 상태 변경이 가능
- 리덕스에도 액션이라는 객체를 통해서만 상태 변경이 가능

*액션: 앱에서 스토어에 운반할 데이터

**Changes are made with pure functions**

- 변경은 순수 함수로만 가능
- 리듀서와 연관되는 개념
- store - action - reducer

*리듀서: 액션을 스토어에 바로 전달하는 것이 아닌 액션을 리듀서에 전달해야함

*리듀서가 주문을 보고 스토어의 상태 업데이트

### 흐름

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/ed08f4e9-4934-479f-a55b-09ffbf96beb6/d5891a30-e8b3-4e10-aaeb-7c25a2c1a45c/image.png)

<aside>
➡️

**Action → Dispatch → Reducer → Store**

</aside>

**Action**

- state를 바꾸는 방식
- 액션 객체를 가짐
- 반드시 type 필드 필요

**Dispatch**

- action을 발생시키는 것
- action 객체를 파라미터로 받음

**Reducer**

- 변화를 일으키는 함수
- action의 결과로 state를 어떤식으로 바꿀지 구체적으로 정의

**Store**

- 프로젝트에 리덕스를 적용하기 위해 필요한 것
- 프로젝트엔 단 한개의 stroe만 가짐
- 상태의 중앙저장소라고 할 수 있음
- reducer, dispatch 등이 스토어의 내장함수로 포함되어있음

<aside>
💡

1. 상태 변경되어야 하는 이벤트 발생시 변경될 상태에 대한 정보가 담긴 action 객체 생성
2. 이 action 객체는 dispatch 함수의 인자로 전달
3. dispatch 함수는 action 객체를 reducer 함수로 전달
4. reducer 함수는 action 객체의 값 확인 후 그 값에 따라 전역 상태 저장소 store 상태 변경
5. 상태가 변경되면 react는 화면 재렌더링
</aside>

### 장점

- 순수 함수를 사용해 **상태를 예측 가능**하게 만듦
- **유지보수**에 용이
- redux dev tool이 있어 **디버깅에 유리**
- 비동기를 지원하는 Redux Saga, Redux Thunk 등 **다양한 미들웨어**가 존재
- 액션에 따른 **모든 변경 추적 가능**

### 단점

- 코드를 작성하는 **가장 짧거나 빠른 방법은 아님**
- **배워야 할 개념**과 **작성해야 할 코드**가 많음
- 리덕스를 유용하게 사용하려면 **많은 패키지 추가**해야함

### 사용하는 이유

- **미들웨어**
    - 미들웨어를 통해 비동기 작업에 대한 좀 더 디테일하고 편한 컨트롤 가능
    - ex: Redux-saga
        - 요청을 연달아 여러번 하게 될 때 이전 요청은 무시하고 마지막 요청만 처리하고 싶을 때
        - 특정 조건이 만족됐을 때 이전에 시작한 요청을 취소하는 상황
        - 컴포넌트 밖에서 어떤 작업을 수행할 때
- **서버 사이드 렌더링**
    - api 요청 결과를 사용해 서버 사이드 렌더링을 할 때 유용 (미들웨어가 유용)
- **테스팅이 용이**
    - 리덕스를 사용한 앱은 테스트 하기가 비교적 쉬움

### Recoil과 차이

> **장단점**
> 

**Recoil**

**장점**

- 직관적이면서 간단한 구조
- 코드의 양이 매우 줄어들게 됌

**단점**

- redux는 안정적인 devtool임

**결론**

- 디버깅의 측면에서 보면 리덕스가 유리

**Redux**

**장점**

- 검증된 신뢰성 있는 라이브러리
- redux devtools로 직관적으로 볼 수 있는 방법 제공
- 상태값이 많아질 경우 디버깅이 상대적으로 recoil에 비해 편해질 것

**단점**

- 작은 상태 하나를 변경하려고 해도 보일러 플레이트 코드를 많이 작성해야하는 번거로움이 있음

**결론**

- Recoil에 비해 상대적으로 코드를 작성하는 양 많아짐

> **비동기 처리**
> 

**Recoil**

- Selector를 사용
- Selector는 recoil에서 비동기 처리를 위해 사용하며 기본적으로 값 캐싱
- 같은 응답을 보내는 api call엔 추가적으로 요청하지 않아 성능적으로 유리
- redux처럼 따로 미들웨어 설치할 필요 x

**Redux**

- redux-thunk, redux-saga, redux-toolkit 같은 미들웨어는 검증된 미들웨어라 신뢰성이 높음
- redux-saga를 사용하면 제너레이터와 이펙트 등의 이해 필요
- 두 상태관리 라이브러리 모두 러닝커브가 생김

### Context api와 차이

> Redux도 Context API를 가지고 만든 라이브러리
> 

→ 전역 상태 관리 측면에선 차이점이 거의 없음

→ Redux는 Context API와 다르게 **전역 상태 관리 외의 다양한 기능 제공**

<aside>
💡

**오직 전역 상태 관리**를 원한다면 **Context Api**

**상태 관리 외에 여러 기능**이 필요하다면 **Redux**

</aside>
