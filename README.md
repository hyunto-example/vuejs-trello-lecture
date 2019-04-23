# 트렐로 개발을 통한 Vuejs, Vuex, Vue-Router 프론트엔드 실전 기술

[인프런 - 트렐로 개발을 통한 Vuejs, Vuex, Vue-Router 프론트엔드 실전 기술 (김정환 강사)](https://www.inflearn.com/course/vuejs/)

## 사용 기술

- Vue.js
- Vuex
- Vue-Router
- Axios
- Dragular

## 분석

### 요구사항 분석

- 인증
  - 로그인
    - 실패시 에러 메세지 출력
  - 로그아웃
- 메인 페이지
  - 보드 목록
  - 보드 생성
    - 보드 입력 폼 - 보드 색상 선택
- 보드
  - 리스트
    - 리스트 출력
    - 리스트 내에 카드 출력
    - 리스트 추가
    - 리스트 제거
    - 리스트 이름 수정
    - 리스트 순서 변경
  - 카드
    - 카드 생성
    - 카드 내용 출력 - 모달
    - 카드 내용 수정
    - 카드 삭제
    - 리스트 내에서 카드 순서 변경
    - 각 리스트 간 카드 이동
  - 사이드바
    - 사이드바 보이기 / 안보이기
    - 보드 배경 변경
    - 보드 삭제

### 기본 플로우

1. 홈페이지 접속
2. 로그인 페이지
3. 홈페이지 리다이렉트
4. 보드 목록 조회
5. 보드 생성
6. 보드 조회 : Todo, Doing, Done 리스트 생성
7. 카드 생성
8. 카드 상세 조회 (모달)
9. 카드 수정 (모달)
10. 카드 이동
11. 카드 삭제
12. 보드 설정 : 배경
13. 보드 삭제 후 홈페이지 이동

### 추가 기능

- 보드 수정 : 색상 변경
- 보드 수정 : 타이틀 변경
- 리스트 생성
- 리스트 수정 : 타이틀 변경
- 리스트 이동
- 리스트 삭제

## 코드 스캐폴딩

### 프로젝트 생성

```bash
$ npm install -g @vue/cli
$ vue create vuejs-trello-lecture
	Vue CLI v3.6.3
	? Please pick a preset: default (babel, eslint)
	...생략...
 
$ npm run serve
```

### 프로젝트 사용법

To customize configuration, See [Configuration Reference](https://cli.vuejs.org/config/).

```bash
## Project setup
npm install

### Compiles and hot-reloads for development
npm run serve

### Compiles and minifies for production
npm run build

### Run your tests
npm run test

### Lints and fixes files
npm run lint
```

# 라우팅

## 라우터의 필요성

라우터의 종류

* 서버 라우팅 : 매 요청마다 화면 갱신
* 브라우저 라우팅 : 매 요청마다 화면을 갱신하지 않고, 필요한 데이터를 요청

## Router 직접 구성

```javascript
/* main.js */
import Vue from 'vue'
import App from './App.vue'

Vue.config.productionTip = false;

const Login = { template: '<div>Login Page</div>' };
const NotFound = { template: '<div>Page not found</div>' };

const routes = {
  '/': App,
  '/login': Login
};

new Vue({
  computed: {
    VueComponent() {
      return routes[window.location.pathname] || NotFound;
    }
  },
  render(h) {
    return h(this.VueComponent);
  }
}).$mount('#app');
```

> 만약 Vue-Cli 버전 3 이상으로 프로젝트를 구성했을 경우, runtimeCompiler 설정의 기본값이 false이기 때문에 위 코드와 같이 HTML 문법을 template에 지정해서 사용할 수 없다.
>
> 따라서 프로젝트 Root 디렉토리에 vue.config.js 파일을 만든 후 설정을 변경해 줘야 한다.
> 참고로 vue.config.js 파일은 @vue/vue-service에 의해 자동으로 로드된다.
>
> ```javascript
> /* vue.config.js */
> //  https://cli.vuejs.org/config/#vue-config-js 
> module.exports = {
>   runtimeCompiler: true
> }
> ```
>
> 

## Vue-Router 구성

### Vue-Router 설치

```bash
$ npm install vue-router --save
```

### Vue-Router 구성

```javascript
/* main.js */
import Vue from 'vue';
import App from './App.vue';

/**
 * Vue-Router 임포트
 */
import VueRouter from 'vue-router';
Vue.use(VueRouter);		// 미들웨어. import 한 vue-router를 사용할 수 있도록 설정한다.

Vue.config.productionTip = false;

const Login = { template: '<div>Login Page</div>' };
const NotFound = { template: '<div>Page not found</div>' };

/**
 * Vue-Router 설정
 */
const router = new VueRouter({
  mode: 'history',
  routes: [
    { path: '/', component: App },
    { path: '/login', component: Login },
    { path: '*', component: NotFound }
  ]
});

new Vue({
  router,		// Vue-Router 설정 적용
  render: h => h({ template: '<router-view></router-view>' })		// 렌더링 변경
}).$mount('#app');
```

## Vue-Router 인스턴스

현재 라우팅 로직이 main.js에 포함되어 있다. 라우팅 로직을 별도의 파일로 분리해서 관리하도록 수정한다.

```bash
## 프로젝트 Root 디렉토리에서
$ mkdir src/router
$ touch src/router/index.js
```

main.js에 포함된 라우팅 로직을 src/router/index.js로 옮긴 후 main.js에서 이 파일을 import 하여 사용하도록 설정한다.
이를 통해 별도의 파일에서 라우팅 로직을 관리할 수 있다. 또한 다수의 파일로도 관리가 가능하다.

```javascript
/* main.js */
import Vue from 'vue';
import router from './router';

Vue.config.productionTip = false;

new Vue({
  router,
  render: h => h({ template: '<router-view></router-view>' })
}).$mount('#app');
```

```javascript
/* router/index.js */
import Vue from 'vue';
import App from '../App.vue';
import VueRouter from 'vue-router';

Vue.use(VueRouter);

const Login = { template: '<div>Login Page</div>' };
const NotFound = { template: '<div>Page not found</div>' };

const router = new VueRouter({
  mode: 'history',
  routes: [
    { path: '/', component: App },
    { path: '/login', component: Login },
    { path: '*', component: NotFound }
  ]
});

export default router;
```





