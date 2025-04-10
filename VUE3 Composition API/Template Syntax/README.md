# Vue Template Syntax
Vue 템플릿 문법은 DOM과 컴포넌트의 데이터를 **선언적으로 바인딩**할 수 있게 해준다.

---

## 텍스트 보간
가장 기본적인 데이터 바인딩은 `{{ data }}` 형태이다.
```vue
<template>
  <p>문자열: {{ message }}</p>
</template>

<script setup>
import { ref } from 'vue'
const message = ref('안녕하세요')
</script>
```

### 일회성 보간: `v-once`
데이터가 변경되어도 **갱신되지 않도록** 하고 싶을때 사용한다.
```vue
<p v-once>문자열: {{ message }}</p>
```

---

## HTML 출력: `v-html`
기본적으로 `{{ }}`는 HTML 태그를 문자열로 해석한다. 실제 HTML을 출력하려면 `v-html`을 사용한다.
```html
<h2>텍스트: {{ rawHtml }}</h2>
<h2>v-html: <span v-html="rawHtml"></span></h2>
```
>⚠️ 주의: v-html은 XSS 공격에 취약하다. 반드시 신뢰된 콘텐츠에서만 사용해야 하며, 사용자 입력값에는 절대 사용하지 말 것.

---

## 속성 바인딩: `v-bind`
HTML 속성에 데이터를 바인딩 하려면 `v-bind`를 사용한다.
```html
<div v-bind:title="dynamicTitle">마우스를 올려보세요.</div>
```
### 불리언 속성
```html
<input type="text" v-bind:disabled="isInputDisabled" />

```
### 단축 문법
```html
<div :title="dynamicTitle">마우스를 올려보세요.</div>
<input type="text" :disabled="isInputDisabled" />
```
### 다중 속성 바인딩
```js
const attrs = {
  id: 'password-id',
  type: 'password',
  placeholder: '비밀번호를 입력해주세요'
}
```
```vue
<input v-bind="attrs" />
```

---

## JavaScript 표현식
모든 바인딩 영역에서는 JS 표현식을 사용할 수 있다.
```vue
{{ isInputDisabled ? '예' : '아니오' }}
{{ message.split('').reverse().join('') }}
<input :placeholder="`입력해주세요 ${isInputDisabled}`" />
```
함수 호출도 가능하다.
```vue
<div>{{ toDay() }}</div>
```