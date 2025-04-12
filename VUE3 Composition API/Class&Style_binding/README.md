# Vue 3 - 클래스(Class)와 스타일(Style) 바인딩

Vue에서는 `:class` 와 `:style` 디렉티브를 통해 동적으로 클래스를 적용하거나 스타일을 지정할 수 있습니다.

---

## 1. 클래스 바인딩

### ✔ 객체(Object) 바인딩

```vue
<div class="text" :class="{ active: isActive, 'text-danger': hasError }"></div>
```
- `active` 클래스는 `isActive`가 `true`일 때 적용됨
- `text-danger` 클래스는 `hasError`가 `true`일 때 적용됨
- 일반 class 속성과 함께 사용 가능

---

### ✔ Computed  객체 바인딩
```vue
<div class="text" :class="classObject"></div>
```
```js
const classObject = computed(() => {
  return {
    active: isActive.value && !hasError.value,
    'text-danger': !isActive.value && hasError.value,
  };
});
```
- 클래스  로직을 `computed`로 분리하면 코드가 더 깔끔해지고 유지보수가 쉬워짐

---

### ✔ 배열(Array) 바인딩
```js
const activeClass = ref('active');
const errorClass = ref('text-danger');
```
```vue
<div :class="[activeClass, errorClass]"></div>
```
- 여러 클래스를 리스트로 한 번에 적용 가능

---

## 2. 스타일 바인딩
### ✔ 객체(Object) 바인딩
```js
const activeColor = ref('red');
const fontSize = ref(30);
```
```vue
<div :style="{ color: activeColor, fontSize: fontSize + 'px' }"></div>
```
- `ref` 값을 이용해 동적으로 스타일 지정 가능


### ✔ 스타일 객체 바인딩
```js
const styleObject = reactive({
  color: 'red',
  fontSize: '13px'
});
```
```vue
<div :style="styleObject"></div>
```
- 객체 자체를 바인딩하여 템플릿을 간결하게 구성 가능


### ✔ 배열(Array) 바인딩
```vue
<div :style="[baseStyles, overridingStyles]"></div>
```
- 여러 스타일 객체를 배열로 묶어 바인딩 가능
- 중복된 스타일 속성은 나중 객체가 우선 적용됨

---

## 정리
| 구분          | 방식       | 설명                                 |
|---------------|------------|--------------------------------------|
| 클래스 바인딩 | 객체       | `:class="{ active: isActive }`       |
|               | 배열       | `:class="[activeClass, errorClass]"` |
|               | computed   | `:class="computedClassObject"`       |
| 스타일 바인딩 | 객체       | `:style="{ color: colorRef }"`       |
|               | 스타일 객체| `:style="styleObject"`               |
|               | 배열       | `:style="[base, override]"`          |