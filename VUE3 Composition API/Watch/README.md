## Watch

Vue에서는 반응형 상태가 변경될 때 특정 작업을 수행해야 하는 경우가 자주 발생한다. 이를 위해 Composition API의 `watch` 함수를 사용하면 된다.

```js
const message = ref('Hello World');

watch(message, (newValue, oldValue) => {
  console.log('newValue: ', newValue);
  console.log('oldValue: ', oldValue);
});
```

---

### Watch의 첫 번째 인자(Source Type)

`watch`의 첫 번째 인자는 다양한 타입이 될 수 있다. `ref`, `reactive`, `computed`, `getter 함수`, `array` 타입이 가능하다.

```js
const x = ref(0);
const y = ref(0);

// 단일 ref
watch(x, (newX) => {
  console.log(`x is ${newX}`);
});

// getter
watch(
  () => x.value + y.value,
  (sum) => {
    console.log(`sum of x + y is: ${sum}`);
  }
);

// 여러 개의 source 배열
watch([x, () => y.value], ([newX, newY]) => {
  console.log(`x is ${newX} and y is ${newY}`);
});
```

`reactive` 객체의 속성은 직접 감시할 수 없고, getter 함수를 사용해야 한다.

```js
const obj = reactive({ count: 0 });

// 잘못된 방식
watch(obj.count, (newValue) => {
  console.log('newValue: ', newValue);
});

// 올바른 방식
watch(() => obj.count, (newValue) => {
  console.log('newValue: ', newValue);
});
```

---

### deep 옵션

`reactive` 객체를 직접 감시하면 암시적으로 깊은 감시자가 생성되어 모든 중첩된 속성도 감시 대상이 된다.

```js
const person = reactive({
  name: '홍길동',
  age: 30,
  hobby: '운동',
  obj: {
    count: 0,
  },
});

watch(person, (newValue) => {
  console.log('newValue: ', newValue);
});
```

getter를 사용하면 중첩된 속성은 감지되지 않으므로 `deep` 옵션을 사용해야 한다.

```js
watch(
  () => person.obj,
  (newValue) => {
    console.log('newValue: ', newValue);
  },
  { deep: true }
);
```

> 💡 deep 옵션은 큰 데이터 구조에 사용 시 성능에 영향을 줄 수 있으므로 필요한 경우에만 사용하는 것이 좋다.

---

### immediate 옵션

`immediate` 옵션을 사용하면 감시를 시작할 때 콜백이 즉시 실행된다.

```js
const message = ref('Hello World!');
const reverseMessage = ref('');

watch(
  message,
  (newValue) => {
    reverseMessage.value = newValue.split('').reverse().join('');
  },
  {
    immediate: true,
  }
);
```

또는 감시 함수 외부에서 수동으로 즉시 실행할 수도 있다.

```js
const reverseFn = () => {
  reverseMessage.value = message.value.split('').reverse().join('');
};

watch(message, reverseFn);
reverseFn();
```

---

## Computed vs Watch

### computed

```js
const reverseMessage = computed(() =>
  message.value.split('').reverse().join('')
);
```

### watch

```js
watch(
  message,
  (newValue) => {
    reverseMessage.value = newValue.split('').reverse().join('');
  }
);
```

### 어떤 것을 선택해야 하는가

- `computed`: 상태 간 종속 관계를 자동으로 설정하고 계산할 때 사용한다.
- `watch`: 상태가 바뀌는 시점에 특정 액션(API 호출, 라우터 이동 등)을 취할 때 적합하다.

대부분의 경우, 계산된 값을 얻는 목적이라면 `computed`를 사용하는 것이 바람직하다.

---

## WatchEffect

`watchEffect`는 콜백 내부에서 접근하는 반응형 데이터를 자동으로 추적하고, 그 값이 바뀌면 자동으로 콜백을 실행한다. 컴포넌트가 생성될 때 즉시 실행된다.

```js
watchEffect(async () => {
  const { data } = await axios.get(`https://reqres.in/api/users?page=${page.value}`);
  items.value = data.data;
});
```

---

## watch vs watchEffect

| 구분 | watch | watchEffect |
|------|-------|-------------|
| 종속성 추적 | 명시적으로 전달한 source만 추적 | 내부에서 접근한 모든 반응형 속성 자동 추적 |
| 실행 시점 | 변경 시 실행 | 즉시 실행 및 변경 시마다 실행 |
| 사용 용도 | 구체적인 감시 대상 필요 시 | 간편하고 자동적인 반응형 추적 필요 시 |

---

> 정리하자면, 단순한 계산 로직은 `computed`, 상태 변경 후 작업은 `watch`, 즉시 실행 및 자동 추적이 필요한 경우는 `watchEffect`를 사용하는 것이 좋다.