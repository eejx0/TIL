# CSS Animation

### @keyframe

1. CSS로 키프레임 블록 만들기
    
    ```css
    @keyframse animationName {
    	0% { /* from으로 작성 가능 */
    		CSS속성 : 속성값;
    	}
    	50% { 
    		CSS속성 : 속성값;
    	}
    	100% { /* to로 작성 가능 */
    		CSS속성 : 속성값;
    	}
    }
    ```
    
    ```css
    @keyframes lotate {
    	0% {
    		transform : rotate(0deg)
    	}
    	50% {
    		transform : rotate(180deg)
    	}
    	100% {
    		transform : rotate(360deg)
    	}
    }
    ```
    

### animation 속성

**animation-name**

- 애니메이션의 중간 상태를 지정하는 이름
- animation 속성의 첫 번째 값 or animation-name이라는 속성
- `animation: lotate;` or `animation-name: lotate;`

**animation-duration**

- 한 사이클의 애니메이션이 재생될 시간 지정
- animation 속성의 두 번째 값 or animation-duration이라는 속성
- 시간 단위로 작성
- 작성하지 않을 경우 기본 값이 0이라 애니메이션 재생 x
    
    ```css
    @keyframes lotate {
    	0% {
    		transform : rotate(0deg)
    	}
    	50% {
    		transform : rotate(180deg)
    	}
    	100% {
    		transform : rotate(360deg)
    	}
    }
    #square {
    	width: 100px;
    	height: 100px;
    	background: pink;
    	margin: 7em;
    	
    	animation-name: lotate;
    	animation-duration: 3s;
    }
    ```
    

**animation-delay**

- 애니메이션이 시작을 지연시킬 시간 지정
- animation-delay라는 속성으로 시간 단위에 맞춰 작성
- animation-duration 코드에서 `animation-delay: 3s` 작성 시 3초 뒤에 정사각형이 3초동안 360도 돔

**animation-direction**

- 애니메이션 재생 방향 지정
- 전달해줄 수 있는 값
    - nomal: 기본 값, 재생이 끝나면 처음부터 다시 재생
    - reverse: 역방향으로 재생
    - alternate: 순방향부터 역방향 번갈아가며 재생
    - alternate-reverse: 역방향부터 순방향 번갈아가며 재생

**animation-iteration-count**

- 애니메이션이 몇 번 반복될지 지정
- 기본 값은 1, 설정한 횟수만큼 애니메이션이 반복 재생됌
- infinite로 설정할 경우 무한 반복
- 소수점 작성할 경우 재생 도중 처음 상태로 돌아감

**animation-play-state**

- 애니메이션 재생 상태 (멈추거나 다시 재생 가능)
- 기본 값은 running, 애니메이션 정지시키는 pause 값으로 지정 가능

**animation-timing-function**

- 애니메이션의 진행 속도 설정
- 중간 상태들의 전환을 어떤 시간간격으로 진행할지 지정
    
    ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/ed08f4e9-4934-479f-a55b-09ffbf96beb6/4639f953-ecdd-42ca-8bc3-afc7f2b691cf/Untitled.png)
    

**animation-fill-mode**

- 애니메이션이 재생 전 후의 상태 지정
    - none: 기본 값, 재생 중이 아닌 경우 요소의 스타일 유지
    - forwards: 재생 중이 아닌 경우 마지막 키프레임 스타일 유지
    - backwards: 재생 중이 아닌 경우 첫 번째 키프레임 스타일 유지
    - both: 재생 전엔 첫 번째 키프레임 스타일, 재생 후엔 마지막 키프레임 스타일 유지
