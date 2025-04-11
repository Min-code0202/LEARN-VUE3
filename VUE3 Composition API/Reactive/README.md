## Vue3 반응형 시스템 정리
### `reactive()` - 객체를 반응형으로 만들기
- `reactive()`: 객체 타입만 가능 (`object`, `array`, `map`, `set` 등)
- **깊은 반응형(Deep Reactive)** 지원: 중첩된 값까지 반응형으로 변환
- 템플릿에서 사용하려면 `setup()`에서 return 해야함
```js
import { reactive } from 'vue'

export default {
  setup() {
    const state = reactive({ count: 0 })
    return { state }
  }
}
```
```html
<!-- 템플릿 -->
<div>{{ state.count }}</div>
```

---

### `ref()` - 원시값을 반응형으로 만들기
- 숫자, 문자열 등 **primitive type**은 `ref()`를 사용해야함
- `.value`를 통해 접근 및 갱신
- 템플릿에서는 `.value` 생략 가능 (자동 unwrapping)
```js
const count = ref(0)
count.value++ // 스크립트에서
```
```html
<!-- 템플릿에서는 .value 생략 -->
<span>{{ count }}</span>
<button @click="count++">증가</button>
```

---

### `ref`와 `reactive` 혼용 시 Unwrapping
- `reactive`에 `ref`를 넣으면 **자동 `.value` 언래핑됨**
```js
const count = ref(0)
const state = reactive({ count })

count.value++
console.log(state.count) // 1
```
> 하지만 배열, Map 등 컬렉션 내부는 자동 언랙핑 ❌
```js
const books = reactive([ref('Vue 3 Guide')])
console.log(books[0].value) // .value 필요
```

---

### 구조 분해 시 반응성 유지하려면 `toRefs()`, `toRef()`
- 구조 분해 하면 반응성 사라짐
- 해결: `toRef()` → 객체 전체 / `toRef()` → 특정 속성
```js
import { reactive, toRefs } from 'vue'

const book = reactive({
  title: 'Vue 3 Guide',
  author: 'Vue Team'
})

const { title } = toRefs(book)
title.value = 'New Title'
console.log(book.title) // 반영됨
```

---

### `readonly()` - 읽기 전용 반응형 객체 만들기
- 변경을 막고 싶을 때 사용
- 내부적으로 반응형 연결은 유지됨
```js
const state = reactive({ count: 0 })
const safeState = readonly(state)

safeState.count++ // 경고: 읽기 전용입니다.
```

---

### `Reactivity Transform` (실험적 기능)
- `ref`의 `.value` 생략 가능하게 해주는 컴파일 타임 기능
- `$ref`, `$computed`, `$watch` 등의 매크로 사용
```vue
<script setup>
let count = $ref(0)
function increment() {
  count++ // .value 없이 가능
}
</script>
```
> 이 기능은 실험적이ㅕ `vue-macros` 또는 `Volar`, `Vite` 설정이 필요함

---

### 요약
| 기능           | 목적                 | 특징                                         |
|----------------|----------------------|----------------------------------------------|
| `reactive()`   | 객체 반응형          | 깊은 반응형, 구조분해 시 반응성 손실         |
| `ref()`        | 원시값 반응형        | `.value`로 접근, 템플릿에서는 생략 가능      |
| `toRefs()`, `toRef()` | 구조분해 반응성 유지 | 각 속성을 `ref`로 변환                       |
| `readonly()`   | 변경 금지 반응형     | 내부 반응성 유지                             |
| `$ref` *(실험적)* | `.value` 없이 사용  | 컴파일 타임 트랜스폼                         |