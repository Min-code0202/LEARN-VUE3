## 목록 렌더링 (v-for)
Vue에서는 v-for 디렉티브를 사용해 배열이나 객체를 반복 렌더링할 수 있다.

### 배열 렌더링
```js
const items = reactive([
  { id: 1, message: 'Java' },
  { id: 2, message: 'HTML' },
  { id: 3, message: 'CSS' },
  { id: 4, message: 'JavaScript' },
]);
```
```html
<ul>
  <li v-for="(item, index) in items" :key="item.id">
    {{ index }} - {{ item.message }}
  </li>
</ul>
```
✅ 포인트
- `v-for="item in items"`  
→ items 배열을 순회하면서 각 요소를 item에 바인딩
- `v-for="(item, index) in items"`  
→ 인덱스도 함께 가져올 수 있음
- `:key="item.id"`  
→ 각 항목에 고유 key 지정 (Vue 2.2.0부터 필수)

---

### 객체 렌더링
```js
const myObject = reactive({
  title: '제목입니다.',
  author: '홍길동',
  publishedAt: '2016-04-10',
});
```
```html
<ul>
  <li v-for="(value, key, index) in myObject" :key="key">
    {{ key }} - {{ value }} - {{ index }}
  </li>
</ul>
```
✅ 포인트
- 객체의 속성 `value`, `key`, `index`를 반복하면서 출력 가능
- `:key="key"`로 고유 식별자 제공

---

## 🔐 :key 사용 시 주의사항
- `:key`는 각 항목을 고유하게 식별하기 위한 필수 속성이다.
- `index`를 `key`로 사용하는 것은 권장되지 않습니다. 가능하면 ***불변의 고유한 ID***를 사용하세요.
