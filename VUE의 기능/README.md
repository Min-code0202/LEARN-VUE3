# VUE의 핵심 기능
Vue의 두 가지 핵심 기능
* 선언적 렌더링(Declarative Rendering): Vue는 템플릿 구문({{ 데이터 }})을 활용하여 선언적으로 출력(렌더링) 할 수 있도록 한다.
* 반응성(Reactivity): Vue는 JavaScript 상태 변경을 자동으로 추적하고 변경이 발생하면 DOM을 효율적으로 업데이트한다.
```
<div id="counter">
        <button type="button" v-on:click="counter++">
            Counter: {{ counter }}</button>
    </div>
    <script>
        const app = Vue.createApp({
            data() {
                return {
                    counter: 100,
                };
            },
        });
        app.mount('#counter');
    </script>
```
따라서 Vue를 사용하면 자바스크립트를 사용하는 것보다 빠르게 애플리케이션을 제작할 수 있다.

## 바인딩(v-bind)
```
<div id="app">
        <input type="text" v-bind:placeholder="message"/> 
    </div>
    <script>
        const app = Vue.createApp({
            data() {
                return {
                    message: '값을 입력해주세요!',
                };
            },
        });
        app.mount('#app');
    </script>
```
위 예제에서 v-bind 속성은 데이터(상태) 속성에 바인딩할 때 사용하는 특수 속성이다. 바인딩 된 DOM은 placeholder 속성을 Vue 인스턴스의 message 속성으로 최신 상태를 유지한다.(반응형 동작)
>v- 접두어가 붙은 특수 속성을 디렉티브(directive)라고 한다.

## 이벤트 핸들링(v-on)
사용자가 앱과 상호 작용할 수 있게 하기 위해 v-on 디렉티브를 사용하여 Vue 인스턴스의 메소드를 호출하는 이벤트 리스너를 추가할 수 있다.
```
<input type="text" v-bind:placeholder="message"/> 
<hr>
<button v-on:click="hello">click</button>
<button v-on:click="reverseMessage">click</button>
```
```
methods: {
              hello(){
                alert("Hello~");
              },
              reverseMessage(){
                this.message = this.message.split('').reverse().join('')
              },
            }
```
이 방법은 직접적으로 DOM(p element)을 건드리지 않고 앱의 상태만 업데이트 한다. 즉 모든 DOM의 조작은 Vue에 의해 처리되고 있다. 

## 양방향 바인딩(v-model)
Vue는 양식(input, select 등)의 입력과 앱의 상태(data)를 양방향으로 바인딩하는 v-model 디렉티브를 제공한다.
```
{{username}}
<input type="text" v-model="username" />
```

## 조건문
엘리먼트 표시여부는 v-if 특수 속성(디렉티브)으로 제어할 수 있다.
```
<p v-if="visible">보이나요?</p>
<button type="button" v-on:click="visible = true">visible</button>
```

## 반복문
v-for는 배열에서 데이터를 가져와 아이템 목록을 표시하는데 사용할 수 있다.
```
<li v-for="item in items">{{ item }}</li>
```
