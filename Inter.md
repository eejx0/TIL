# 타입스크립트의 inter 키워드
> **조건부 타입에서 특정 타입을 추론**하는 데 사용
> 

→ 타입을 직접 지정하는 것이 아닌 타입스크립트가 해당 타입을 유추할 수 있도록 도움

- extends를 사용하는 조건부 타입 안에서 활용
- 특정 타입을 분해해 사용 가능

```tsx
type ReturnType<T> = T extends (...args: any[]) => infer R ? R : never;

function getAge() {
  return 19;
}

type Age = ReturnType<typeof getAge>; 

const age: Age = 19; // 정상
```

- inter R로 T가 함수타입이면 그 반환 타입을 R로 추론, 아니면 never 반환
- getAge 함수의 반환 타입 추출
- const age: Age = "19"  → 오류

### extends

<aside>
✅

**용도**

---

- 제네릭에서 타입을 제한하는 역할
- 조건부 타입에서 특정 타입이 다른 타입을 포함하는지 확인
</aside>
