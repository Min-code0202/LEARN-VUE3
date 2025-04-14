## 조건부 렌더링 (Vue 3)
### v-if
조건이 true일 때만 해당 엘리먼트를 렌더링함.

```html
<h1 v-if="visible">Hello Vue3!</h1>
```

---

### v-else
v-if 조건이 false일 때 렌더링됨. v-if 바로 다음 요소여야 함.

```html
<h1 v-if="visible">Hello Vue3!</h1>
<h1 v-else>Good bye!</h1>
```

---

### v-else-if
여러 조건 분기 처리 시 사용 (else if 역할)

```html
<h1 v-if="type === 'A'">A</h1>
<h1 v-else-if="type === 'B'">B</h1>
<h1 v-else-if="type === 'C'">C</h1>
<h1 v-else>Not A/B/C</h1>
```

---

### `<template v-if="">`
여러 태그를 조건부로 묶고 싶을 때 사용.

```html
<template v-if="visible">
  <h1>Title</h1>
  <p>Paragraph 1</p>
  <p>Paragraph 2</p>
</template>
```

---

### v-show
항상 DOM에는 렌더링됨. display: none을 통해 보이기/숨기기만 제어.

```html
<h1 v-show="show">Title</h1>
<button @click="show = !show">toggle show</button>
```

---

## `v-if` vs `v-show` 비교표

| 구분         | `v-if`                                        | `v-show`                                       |
|--------------|-----------------------------------------------|------------------------------------------------|
| **렌더링 방식** | 조건이 `true`일 때만 DOM에 추가됨              | 항상 DOM에 존재하고 CSS로 토글                  |
| **성능**       | 초기 렌더링에 유리 (조건이 자주 안 바뀔 때)      | 빈번한 토글에 유리                              |
| **트리거**     | DOM 생성 / 제거                               | CSS `display` 속성만 변경                       |
| **특징**       | Lazy (조건이 `true`일 때 최초 렌더링됨)         | 초기 렌더링 시 무조건 렌더링됨                  |

---

## ⚠️ `v-if`와 `v-for` 함께 쓰는 건 비추천

- `v-if`가 `v-for`보다 우선순위가 높기 때문에 **의도치 않은 결과**가 나올 수 있음.
- [📘 Vue Style Guide - v-if와 v-for](https://v3.ko.vuejs.org/style-guide/#v-if%E1%84%8B%E1%85%AA-v-for-%E1%84%83%E1%85%A9%E1%86%BC%E1%84%89%E1%85%B5-%E1%84%89%E1%85%A1%E1%84%8B%E1%85%AD%E1%86%BC-%E1%84%91%E1%85%B5%E1%84%92%E1%85%A1%E1%84%80%E1)
