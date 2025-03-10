# React query
> **서버에서 데이터를 가져오는(fetch), 캐싱하는(cache), 동기화하는(sync)걸 자동으로 해주는 라이브러리**
> 

→ 서버에서 데이터를 가져오고 캐싱하고 동기화하고 업데이트하는 작업을 쉽게 도와주는 도구

### 필요한 이유

```tsx
const [data, setData] = useState(null);
const [loading, setLoading] = useState(true);
const [error, setError] = useState(null);

useEffect(() => {
    const fetchData = async () => {
      try {
        const response = await axios.get("https://api.example.com/data");
        setData(response.data);
      } catch (err) {
        setError(err);
      } finally {
        setLoading(false);
      }
    };
    fetchData();
  }, []);
```

**이 방식의 문제점** 🤔

- 로딩, 에러, 데이터 상태를 직접 관리해야함 (useState로 직접 상태 저장)
- 데이터를 다시 가져오려면(refetch) 또 useEffect를 사용해야 함
- 캐싱이 없어서 같은 데이터를 다시 요청하면 불필요한 네트워크 호출 발생

→ **React Query 두둥 등장**

```tsx
import { useQuery } from "@tanstack/react-query";

// 컴포넌트 밖에서
const fetchData = async () => {
  const { data } = await axios.get("https://api.example.com/data");
  return data;
};

// 컴포넌트 안에서
const { data, isLoading, error } = useQuery({
  queryKey: ["myData"], // 캐싱 키
  queryFn: fetchData,    // API 호출 함수
});
```

### 장점

<aside>
✅

**자동 캐싱**

---

같은 데이터를 여러번 요청해도 캐시에서 가져오기 때문에 불필요한 api 호출 ⬇️

</aside>

<aside>
✅

**자동 리패치(새로고침)**

---

컴포넌트가 다시 마운트되면 자동으로 최신 데이터를 가져옴

```tsx
const { data, refetch } = useQuery({
  queryKey: ["myData"],
  queryFn: fetchData,
});

<button onClick={() => refetch()}>다시 불러오기</button>
// 버튼 누르면 api 다시 호출해서 최신 데이터 가져옴
```

</aside>

<aside>
✅

**쉬운 refetch(데이터 갱신)**

---

refetch() 함수 하나만 호출하면 데이터를 다시 불러올 수 있음

</aside>

<aside>
✅

**에러 핸들링 내장**

---

error 상태를 바로 받을 수 있어서 try-catch를 직접 쓰지 않아도 됌

</aside>

<aside>
✅

**배경 업데이트**

---

기존 데이터를 먼저 보여주고 새로운 데이터를 백그라운드에서 가져와 업데이트

</aside>

<aside>
✅

**자동 garbage Collection**

---

사용하지 않는 데이터는 자동으로 메모리에서 제거됨

</aside>

### 핵심 개념

| **기능** | **설명** |
| --- | --- |
| `useQuery` | 데이터 가져오기 |
| `useMutation` | 데이터 추가/수정/삭제 |
| `queryKey` | 데이터를 식별하는 키 |
| `queryFn` | 실제 데이터를 가져오는 함수 |
| `refetch` | 수동으로 데이터를 다시 불러옴 |
| `invalidateQueries` | 기존 데이터를 무효화하고 새로운 데이터 요청 |
