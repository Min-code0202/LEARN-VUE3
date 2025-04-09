# Vue 설치방법
Vue를 설치할 수 있는 방법은 크게 3가지가 있다.
* 페이지에 <U>**CDN**</U> package로 import하기
* <U>**npm**</U>을 사용하여 import하기
* 공식 <U>**CLI**</U>을 사용하여 프로젝트를 scaffold하고, 최신 프론트엔드 워크플로우(hot-reload, lint-on-save 등)를 위한 batteries-included build 제공
>scaffold란? 개발을 용이하게 시작할 수 있는 발판을 제공해주는 것을 말한다.   
batteries-included란? 외부 라이브러리를 더하지 않아도 기본적으로 제공하는 표준 라이브러리만으로도 시작하는데 문제 없다는 의미로 해석할 수 있다.
  
## CDN
프로토타이핑 또는 학습 목적이라면, 아래 코드로 최신 버전을 사용할 수 있다.
```js
<script src="https://unpkg.com/vue@next"></script>
<!-- 또는 -->
<script src="https://unpkg.com/vue@3.2.31"></script>
```
  
## npm
Vue를 사용하여 대규모 애플리케이션을 구축할 때 NPM을 이용한 설치를 권장하고 있다. NPM은 Webpack 또는 Browserify와 같은 모듈 번들리와 잘 작동한다.
```bash
npm install vue@3.1.9 // 
<!-- 최신버전 -->
npm install vue
```
  
## Vue CLI
Vue CLI은 웹팩 기반 빌드도구이다. 하지만 Vue CLI는 현재 유지관리 모드에 있다. 특정 웹팩 기능에 의존하지 않는 한 Vite로 새 프로젝트를 시작하는 것을 권장한다.  
Vue CLI을 사용하기 위해 `@vue/cli` v4.5 이상의 버전을 설치해야 한다.
```bash
npm install -g @vue/cli
```
  
## Vite
<U>Vite</U>는 Vue SFC를 지원하고 매우 가볍고 빠른 빌드 도구이다.  
Vite는 개발 서버를 구동할 때 매우 빠르다. 또한 소스 코드 변경이 일어났을 때 전체 모듈을 번들링 하는것이 아닌 변경된 모듈만 교체하기 때문에 개발을 더욱더 빠르게 진행할 수 있다.
```bash
npm init vue@@lastest

cd {product name}
npm install
npm run dev
```
이 명령은 공식 Vue 프로젝트 스캐폴딩 도구인 create-vue를 설치하고 실행한다.