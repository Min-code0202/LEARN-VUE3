# Setup
`setup()` 함수는 Composition API 사용의 진입점이며, 컴포넌트 인스턴스가 생성되기 전에 실행된다.

## 기본 사용
`setup()` 내에서 반응형 API(`ref`, `reactive` 등)를 이용해 상태를 선언하고, 객체를 반환해 `<template>`에서 사용할 수 있다.
```js
<script>
import { ref } from 'vue'

export default {
  setup() {
    const count = ref(0)
    return { count }
  },
  mounted() {
    console.log(this.count) // 0
  }
}
</script>

<template>
  <button @click="count++">{{ count }}</button>
</template>
```

---

## Props 접근
`setup()`의 첫 번째 인자는 `props`이며 반응형 객체이다.
```js
export default {
  props: {
    title: String
  },
  setup(props) {
    console.log(props.title)
  }
}
```
구조 분해 할당 시 반응성을 잃기 때문에 반드기 `props.title`처럼 접근해야 한다.

### 반응성을 유지한 구조 분해: `toRef`, `toRefs`
```js
import { toRefs, toRef } from 'vue'

setup(props) {
  const { title } = toRefs(props) // title.value 사용
  const titleRef = toRef(props, 'title')
}
```

---

## Setup Context
`setup`의 두 번째 인자는 `context`로 다음과 같은 속성을 제공한다.
- `attrs`:`$attrs`와 동일 (비반응형)
- `slots`:`$slots`와 동일 (비반응형)
- `emit`:`$emit`와 동일
- `expost`:컴포넌트 외부에 공개할 속성을 명시적으로 정의
```js
setup(props, { attrs, slots, emit, expose }) {
  // 사용 예시
}
```
> `attrs`와 `slots`는 반응형이 아니므로 구조 분해 할당해도 상관 없음.
단, 업데이트 타이밍에 따라 값이 바뀔 수 있으므로 `onBeforeUpdate` 훅 내에서 사용해야 정확함

---

## expose:컴포넌트 외부 공개 제어
`expose()`를 사용하면 `template refs`를 통해 상위 컴포넌트에 노출되는 속성을 제한할 수 있다.
```js
setup(props, { expose }) {
  const publicCount = ref(0)
  const privateCount = ref(0)

  expose({ count: publicCount })
}
```

---

## Render 함수 사용
`setup()`에서 렌더 함수를 직접 반환할 수 있다. 이 경우 `template`을 사용하지 않는다.
```js
import { h, ref } from 'vue'

export default {
  setup() {
    const count = ref(0)
    return () => h('div', count.value)
  }
}
```
### render + expose
렌더 함수만 사용하는 경우, 메소드를 상위 컴포넌트에 노출하려면 `expose()`를 명시해야 한다.
```js
setup(props, { expose }) {
  const count = ref(0)
  const increment = () => ++count.value

  expose({ increment })

  return () => h('div', count.value)
}
```