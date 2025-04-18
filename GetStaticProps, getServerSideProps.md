# getStaticProps, getServerSideProps
<aside>
🗣

**사전 렌더링이 필요할 때 사용하는 Next.js 내장 기능**

</aside>

### getStaticProps

> 빌드할 때 딱 한번만 실행되는 **정적 사이트 생성 (Static Site Generation)** 함수
> 

- 다시 빌드를 하지않으면 실행되지 않기에 수정될 일이 거의 없는 정적 페이지를 렌더링하기 좋음
- return 문의 내부 파라미터로 revalidate라는 속성을 추가해 업데이트 주기를 전달하면 그 업데이트 주기 단위로 페이지가 재생성되어 다시 빌드를 하지 않아도 props 업데이트 가능
- 동적 페이지를 사전 렌더링하려면 getStaticPaths 함수를 추가해줘야 함

### getServerSideProps

> getStaticProps와 비슷하지만 **서버 사이드 렌더링 (Server Side Rendering)**을 위한 함수
> 

- 요청이 들어올 때마다 호출되고 그 때마다 사전 렌더링을 함
- 빌드 이후 자주 바뀌는 동적 데이터가 들어갈 때 사용하기 좋음
- 매 요청마다 호출되어 성능은 getStaticProps에 뒤치지만 내용을 언제든 동적으로 수정 가능
