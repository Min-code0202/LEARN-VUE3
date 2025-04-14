# v-model 이란?
>`v-model`은 **양방향 바인딩을 쉽게 해주는 Vue 디렉티브**   
입력값을 자바스크립트 변수와 실시간으로 연결해서, 별도로 `@input`과 `:value`를 쓸 필요 없이 편하게 동기화할 수 있다.

```html
<!-- 번거로운 방식 -->
<input :value="text" @input="event => text = event.target.value" />

<!-- v-model을 쓰면 이렇게 간단해짐 -->
<input v-model="text" />
```

---

##  텍스트 입력 요소

### input (텍스트)
```html
<input v-model="text" />
```

### textarea
```html
<textarea v-model="textareaValue"></textarea>
```

---

## 체크박스, 라디오 버튼, 셀렉트

Vue는 요소의 종류에 따라 자동으로 알맞은 속성과 이벤트를 사용할 수 있다.

| 요소        | 속성       | 이벤트      |
|-------------|------------|-------------|
| `input`, `textarea` | `value`     | `input`     |
| `checkbox`, `radio` | `checked`   | `change`    |
| `select`            | `value`     | `change`    |

---

### checkbox

#### 기본: true / false
```html
<label>
  <input type="checkbox" v-model="checkboxValue" />
  {{ checkboxValue }}
</label>
```

#### 여러 개: 배열
```html
<div>
  <label><input type="checkbox" v-model="checkboxValues" value="html" /> HTML</label>
  <label><input type="checkbox" v-model="checkboxValues" value="css" /> CSS</label>
  <label><input type="checkbox" v-model="checkboxValues" value="javascript" /> JavaScript</label>
  <p>{{ checkboxValues }}</p>
</div>
```

#### true-value / false-value
```html
<label>
  <input
    type="checkbox"
    v-model="checkboxYN"
    true-value="Yes"
    false-value="No"
  />
  {{ checkboxYN }}
</label>
```

---

### radio
```html
<label>
  <input type="radio" name="type" value="O" v-model="radioValue" />
  O형
</label>
<label>
  <input type="radio" name="type" value="A" v-model="radioValue" />
  A형
</label>
```

---

### select
```html
<select v-model="selectValue">
  <option value="html">HTML 수업</option>
  <option value="css">CSS 수업</option>
  <option value="javascript">JavaScript 수업</option>
</select>
```

---

## v-model 수식어 (modifiers)

| 수식어      | 설명 |
|-------------|------|
| `.lazy`     | `change` 이벤트 이후 동기화됨 |
| `.number`   | 입력값을 숫자로 자동 형변환 |
| `.trim`     | 앞뒤 공백 제거 |

### 예시
```html
<input v-model.lazy="text" />
<input v-model.number="age" />
<input v-model.trim="name" />
```
