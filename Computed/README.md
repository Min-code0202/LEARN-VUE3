# Vue 3 - Computed 정리

Vue 3에서 `computed` 속성을 활용하면 **템플릿 표현식을 간결하게 만들고**, **성능을 최적화**할 수 있다.

---

## Computed 속성 요약

| 구분          | 설명 |
|---------------|------|
| **용도**      | 템플릿 표현식이 길어질 때 가독성 향상, 로직 재사용 |
| **특징**      | 결과 **자동 캐싱**, 의존하는 값 변경 시에만 다시 계산 |
| **비교**      | `computed`는 **캐시**, `method`는 **항상 실행** |
| **사용법**    | `{{ computedProperty }}` 형태로 템플릿에서 사용 가능 |

---

## 예제 코드 설명

### Reactive 객체 선언

```js
const teacher = reactive({
  name: 'min',
  lectures: ['HTML/CSS', 'JavaScript', 'Vue3']
});
```

---

### Computed vs Method
```js
const hasLecture = computed(() => {
  return teacher.lectures.length > 0 ? '있음' : '없음';
});

const existLecture = () => {
  return teacher.lectures.length > 0 ? '있음' : '없음';
};

```
| 구분          | 설명 |
|---------------|------|
| `hasLecture`    | `computed`, 캐시됨, 의존 값이 바뀔 때만 다시 계산됨 |
| `existLecture()`     | `method`, 호출될 때마다 실행됨 (캐시 없음) |

---

### Writable Computed (읽기/쓰기 가능한 계산된 속성)
```js
const firstName = ref('홍');
const lastName = ref('길동');

const fullName = computed({
  get() {
    return firstName.value + ' ' + lastName.value;
  },
  set(value) {
    [firstName.value, lastName.value] = value.split(' ');
  }
});

fullName.value = ' min';
```

---

### 템플릿 예시
```vue
<template>
  <div>
    <h2>Author가 책을 갖고 있나요?</h2>
    <p>{{ hasLecture }}</p>        <!-- computed -->
    <p>{{ existLecture() }}</p>    <!-- method -->
    <button @click="counter++">counter: {{ counter }}</button>
    <p>{{ fullName }}</p>          <!-- computed with getter/setter -->
  </div>
</template>
```

---

### 요약
- `computed`는 성능이 좋고, 중복 표현식을 깔끔하게 정리할 수 있음
- `method`는 동작은 같지만 항상 새로 계산
- 복잡한 템플릿 표현식은 반드시 computed로 분리하자
- `computed`는 기본 읽기 전용, 필요하면 setter로 쓰기 가능