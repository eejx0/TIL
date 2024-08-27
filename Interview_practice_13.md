## React

### 정의

<aside>
💡 **웹 프레임워크**로 **자바스크립트의 라이브러리**

</aside>

→ facebook에서 제공해주는 프론트엔드 라이브러리

### 왜 사용하는지

1. **컴포넌트 기반 아키텍쳐**
    - **재사용성**
        - React는 컴포넌트 기반으로 설계되어 있음
        - 애플리케이션의 다양한 부분에서 재사용이 가능해 코드 중복을 줄이고 유지보수를 쉽게 할 수 있음
    - **모듈성**
        - 개발자가 특정 부분만 집중적으로 작업 가능
2. **가상 DOM**
    - **빠른 성능**
        - 실제 DOM 대신 가상 DOM을 사용해 변경 사항을 적용
        - 가상 DOM은 변경사항을 메모리에 저장하고 효율적인 업데이트를 위해 필요한 부분만 업데이트
    - **최소한의 리렌더링**
3. **단방향 데이터 흐름**
    - **예측 가능한 데이터 흐름**
        - 데이터의 흐름이 항상 한 방향으로만 이루어지게 함
        - 상태 변화가 예측 가능하고 디버깅이 용이
4. **풍부한 생태계와 커뮤니티**
    - 광범위한 라이브러리와 도구
    - 활발한 커뮤니티 지원
5. **서버 사이드 렌더링 지원**
    - **SEO 향상**
        - React는 Next.js와 같은 프레임워크로 SSR 쉽게 구현 가능
        - SSR은 초기 페이지 로드를 빠르게하고 SEO 성능 향상에 도움을 줌
6. **지속적인 업데이트와 혁신**

### 특징 (장단점)

> **장점**
> 
- React 공식 문서 가이드, 자료를 통해 쉽게 접하고 배우기 가능
- 로직을 분리하는 것이 아닌 Component 하나로 관리
- 성능이 뛰어난 가비지 컬랙터, 메모리 관리 기능 지원
- UI 수정과 재사용성이 좋음
- 코드 가독성 높임
- 다른 framework나 라이브러리와 병행해 사용 가능

> **단점**
> 
- IE8 이하 버전은 지원 x
- view 이외 기능은 직접 구현하거나 라이브러리로 구현해야해서 JS 배경지식이 필수
- 스타일링의 어려움
- 로딩 시간이 김
- 웹의 궁극적 지향점과는 다소 동떨어져 있음

## React 함수 2가지 사용 예시 & 이유

- 사용한 예시 코드 (STIDI)
    
    ```tsx
    import React, { useCallback, useEffect, useState } from "react";
    import styled from "styled-components";
    import Banner1 from "../../assets/Banner.svg";
    import Banner2 from "../../assets/Banner2.svg";
    import LeftButton from "../../assets/LeftButton.svg";
    import RightButton from "../../assets/RightButton.svg";
    
    const banners = [Banner1, Banner2, Banner1];
    
    export const Banner = () => {
        const [currentBanner, setCurrentBanner] = useState(1);
        const [autoSlide, setAutoSlide] = useState(true);
        const goToPreviousBanner = () => {
            setCurrentBanner((currentBanner - 1 + banners.length) % banners.length);
        };
    
        const goToNextBanner = useCallback(() => {
            setCurrentBanner((currentBanner + 1) % banners.length);
        }, [currentBanner]);
    
        const startAutoSlide = () => {
            setAutoSlide(true);
        };
    
        const stopAutoSlide = () => {
            setAutoSlide(false);
        };
    
        // autoSlide와 goToNextBanner 값이 변경될 때마다 useEffect 실행
        useEffect(() => {
            let interval: NodeJS.Timeout | null = null;
            if (autoSlide) {
                interval = setInterval(goToNextBanner, 2000);
            }
            return () => {
                if (interval) {
                    clearInterval(interval);
                }
            };
        }, [autoSlide, goToNextBanner]);
    
        const renderBanners = () => {
            const bannerElements = [];
            for (let index = 0; index < banners.length; index++) {
                bannerElements.push(<BannerImage key={index} src={banners[index]} alt={Banner ${index + 1}} />);
            }
            return bannerElements;
        };
    
        return (
            <BannerWrap onMouseEnter={stopAutoSlide} onMouseLeave={startAutoSlide}>
                <ButtonWrap left onClick={goToPreviousBanner}>
                    <img src={LeftButton} alt="Left Button" />
                </ButtonWrap>
                <ButtonWrap right onClick={goToNextBanner}>
                    <img src={RightButton} alt="Right Button" />
                </ButtonWrap>
                <BannersContainer currentBanner={currentBanner}>{renderBanners()}</BannersContainer>
            </BannerWrap>
        );
    };
    
    const BannerWrap = styled.div
        position: relative;
        display: flex;
        justify-content: center;
        overflow: hidden;
        width: 100%;
        height: 180px;
    ;
    
    const BannersContainer = styled.div<{ currentBanner: number }>
        display: flex;
        transition: transform 0.5s;
        transform: translateX(-${({ currentBanner }) => currentBanner * 100}%);
        width: 70%;
        gap: 10px;
    ;
    
    const BannerImage = styled.img
        flex-shrink: 0;
        width: 100%;
        height: auto;
        cursor: pointer;
    ;
    
    const ButtonWrap = styled.div<{ left?: boolean; right?: boolean }>
        position: absolute;
        top: 50%;
        transform: translateY(-50%);
        width: 62px;
        height: 62px;
        background-color: white;
        border-radius: 50%;
        display: flex;
        align-items: center;
        justify-content: center;
        box-shadow: 0px 3px 7px 3px rgba(0, 0, 0, 0.12);
        cursor: pointer;
        z-index: 1;
        ${({ left }) => left && left: 150px;}
        ${({ right }) => right && right: 150px;}
    
        &:hover {
            transition: 0.2s;
            background-color: #e6e6e6;
        }
    
        @media (max-width: 1200px) {
            width: 40px;
            height: 40px;
            ${({ left }) => left && left: 180px;}
            ${({ right }) => right && right: 180px;}
        }
    ;
    ```
    

### useState

<aside>
💡 useState는 **컴포넌트에서 상태를 관리**하기 위해 사용됨

</aside>

- currentBanner
    - 현재 표시되고 있는 배너의 인덱스를 저장
    - 초기 상태를 1로 설정
    - 배너 슬라이드를 수동으로 변경할 때 이 상태가 업데이트됨
- autoSlide
    - 배너가 자동으로 슬라이드될지 여부 결정
    - useState(true)를 사용해 자동 슬라이드가 기본적으로 활성화되도록 설정
    - 사용자가 배너 위에 마우스 올리면 일시 중지되고 떼면 다시 시작
- **사용하는 이유**
    - 배너 슬라이더의 현재 상태 관리
    - 사용자의 인터렉션(ex: 버튼 클릭, 호버)에 따라 상태 업데이트

### useEffect

<aside>
💡 useEffect는 **컴포넌트가 렌더링될 때나 특정 상태나 값이 변경**될 때마다 **특정 작업을 수행**하도록 하기 위해 사용됨

</aside>

- autoSlide, goToNextBanner가 변경될 때마다 자동 슬라이드 관리
- 활성화된 경우 2초마다 goToNextBanner 함수를 호출해 배너가 자동으로 넘어가도록 설정
- 컴포넌트가 언마운트되거나 autoSlide, goToNextBanner 값이 변경될 때 이전의 타이머 정리를 위해 clearInterval를 호출하는 함수 반환
- **사용하는 이유**
    - 렌더링될 때나 상태가 업데이트 될 때마다 사이드 이펙트 (ex: 자동 슬라이드 기능) 효과적으로 관리
    - 리소스 낭비 x

## React에서 상태관리를 사용하는 이유

<aside>
💡 각 **컴포넌트 간**의 **직접적인 데이터 전달**이 **어려움**
데이터를 부모 컴포넌트에 보내고 다시 해당 상태 데이터를 필요한 컴포넌트로 전달해야함

</aside>

→ props Drilling이 많아질 경우 prop의 출처 찾기 어려움

1. 복잡한 시스템을 다룰 때 필요
    
    상태 관리 없이 진행하면 사용자가 웹 내에서 수행하는 작업의 상태 추적이 어려움
    
2. 프로그램이 어떻게 구동 될지 예측 가능
3. 코드를 추후에 유지보수하는 것에 있어 긍정적인 효과를 줌
    
    상태관리 시 상태를 확인하는 것이 쉬워 문제 발생 시 원인 파악이 쉬움
    
4. 여러 컴포넌트 간의 데이터 공유 용이
    
    중복 코드 방지, 코드 재사용성 증가
    
5. 성능 최적화에 도움
    
    필요한 상태만 업데이트해 불필요한 렌더링, 네트워크 요청 최소화
    

## React LifeCycle

### 정의

생명주기: 컴포넌트가 생성되고 사용되고 소멸될 때 까지 일련의 과정

라이프 사이클 이벤트: 생명주기 안에서 특정 시점에 자동으로 호출되는 메서드

<aside>
💡 React는 라이프 사이클 이벤트를 기반으로 컴포넌트의 동작 제어
컴포넌트의 작업 수행을 향상시키는 사용자 정의 로직 구현 가능

</aside>

→ ex: 라이프 사이클 이벤트 중 재렌더링 여부를 정할 수 있는 이벤트가 있음

→ 이걸 사용하면 불필요하게 렌더링되는 것을 방지해 성능 개선 가능

→ 라이프 사이클 이벤트로 원하는 시점에 서버에서 데이터를 가져와 사용 가능

### LifeCycle 이벤트 진행 순서

![컴포넌트는 생성 → 업데이트 → 제거의 생명주기를 갖는다](https://prod-files-secure.s3.us-west-2.amazonaws.com/ed08f4e9-4934-479f-a55b-09ffbf96beb6/e921c53a-5706-481e-b9e3-0a0eadd28a27/image.png)

컴포넌트는 생성 → 업데이트 → 제거의 생명주기를 갖는다

1. constructor(): 엘리먼트를 생성해 기본 state, prop 설정할 때 실행
2. componentWillMound(): 컴포넌트를 DOM에 삽입하기 전 실행
3. render()
4. componentDidMount(): DOM에 삽입되어 렌더링이 완료된 후 실행
5. componentWillReceiveProps(nextProps): 컴포넌트가 Porps 받기 직전 실행
6. shouldComponentUpdate(nextProps, nextState): 컴포넌트가 갱신되기 전 실행, 렌더링 유무 설정
7. componentWillUpdate(nextProps, nextState): 컴포넌트가 갱신되기 직전 실행
8. render()
9. componenetDidUpdate(prevProps, prevState): 컴포넌트가 갱신된 후 실행
10. componentWillUnmount(): 컴포넌트를 DOM에서 제거하기 전 실행

⇒ 리액트 17부턴 componentWillMount, componentWillUpdate, componentWillReceiveProps 라이프 사이클이 사용되지 않음
