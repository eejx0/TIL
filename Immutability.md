# 불변성 (Immutability)
> **데이터가 최초 생성된 이후 그 상태를 변경할 수 없는 성질**
> 

```tsx
const person = { name: "Nurung", age: 3 };

// 불변성 유지
const updatePerson = { ...person, age: 30 };

console.log(person) // name: "Nurung", age: 3
console.log(updatePerson) // name: "Nurung", age: 30
```

<aside>
✅

**불변성을 유지하기 위해서..**

---

- 스프레드 연산자
- Object.assign(), Object.freeze()같은 내장 기능 사용
</aside>

- 설명
    
    **Object.assign(obj1, obj2):** obj1에 obj2의 값을 덮어씌우며 수정된 obj1이 리턴됨
    
    **Object.freeze()**: 객체를 동결해서 변경할 수 없게 만듦
    
    → 중첩된 객체는 동결되지 않음 🔥
    
    ```tsx
    const person = {
    	name: "Nurung",
    	age: 3,
    	pet: {
    		type: "dog",
    	}
    }
    ```
    

### 성능 면에서  불리하지 않을까?

- **불변성 유지는 장기적으로 유지보수성과 안정성을 크게 향상시킴** ⬆️
- **데이터의 변경 흐름을 추적하기 쉽게 만들어줌** 👍🏻

업데이트마다 새로운 객체를 생성해야 하므로 메모리 비용이 증가할 수 있음 → 근데 무시할만한 수준..
