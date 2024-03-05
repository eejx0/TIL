# useMutation

> React-Query로 서버에 변경 작업 요청 시 사용 (insert, update, delete)
> 

### mutationFn

axios를 이용해 서버에 api 요청

```jsx
const deleteData = useMutation(() => axios.delete(`api/delete/${id}`));

const deleteData = useMuatation({
	mutationFn: (id) => axios.delete(`api/delete/${id}`)
})
```

### mutate

useMutation 이용 → 작성한 내용이 실제로 실행될 수 있도록 도움
이벤트 발생 시 사용

```jsx
const {mutate} = () => deleteData()

const deleteFm = () => {
	deleteData.mutate(id)
}
```

### onSuccess, onError, onSettled

```jsx
const deleteData = async () => {
	try {
		const res = await axios.delete(`api/delete/${id}`)
		.then((res) => console.log(res.data))
	} catch(err) {
		console.error('error', err.message)
	} finally {
		console.log('실행')
	}
}
```

```jsx
// key 값 생략
const deleteData = useMutation((id) => axios.delete(`api/delete/${id}`), {
	onSuccess: () => {console.log('요청 성공')},
	onError: () => {console.log('에러 발생')},
	onSettled: () => {console.log('결과에 상관 x -> 무언가 실행')}
})

// key 값 명시
const deleteData = useMutation({
	mutationFn: (id) => axios.delete(`api/delete/${id}`),
	// onSuccess, onError, onSettled 그대
})
```

### onMutate

성공 시 현재 데이터 캐시 업데이트 or UI 변경
onMutate callback 함수에서 UI 업데이트 후 setQueryData 함수로 이전 데이터 업데이트
