
# [Nuxt](https://ko.nuxtjs.org/)

Vue.js 어플리케이션을 만드는 프레임워크다.
클라이언트/서버 배포를 추상화 하는 동안의 UI 렌더링을 하며, 서버 렌더링도 가능하다.


## 기술 스택
Vue.js + Webpack + Babel

아래 기능들을 포함한다.
- Vue.js
- Vue Router
- Vuex(store 옵션)
- Vue Server Renderer
- vue-meta

## 특징
- Vue 파일 쓰기(.vue)
- SRR
- 비동기 데이터 기반의 라우팅 시스템
- 정적 파일 전송
- ES6/ES7 지원
- JS&CSS 코드 번들링 및 압축
- Hot loader
- 모듈식 아키텍처 확장

## [디렉토리 구조](https://ko.nuxtjs.org/guide/directory-structure)
import시 상대/절대경로로 모두 접근 가능하다.
```vue
import Footer from "../../components/Footer"

// BETTER BELOW
import Footer from  "~/components/Footer"
```

### /assets
LESS, SASS, JS같은 컴파일되지 않은 asset을 포함

### /components
Vue.js 컴포넌트를 포함. /pages 내의 .vue에서 불러다 쓴다.

### /layouts
어플리케이션의 레이아웃 포함

### /middleware
어플리케이션의 미들웨어를 포함. 페이지나 레이아웃이 렌더링되기 전에 실행할 사용자 정의 함수를 정의.

### /pages
어플리케이션의 뷰와 라우트를 포함. Nuxt.js는 해당 디렉토리 내 모든 .vue 파일을 읽고 어플리케이션의 라우터를 생성.
RESTful 한 uri를 만들기 위해서는 아래와 같이 pages 구조를 잡을 수 있다.
```
pages/
ㄴ users/
  ㄴ index.vue    -> /users
  ㄴ _id.vue      -> /users/23
```
`_`는 dynamic route를 의미한다.

### /plugins
루트 vue.js 어플리케이션이 생성되기 전 실행하고 싶은 js 플러그인을 포함.

### /static
정적 파일 포함. 이 디렉토리 내의 파일에 접근할때에는 루트(/)에 연결

### /store
Vuex store 파일 포함

## 비동기 데이터 호출
asyncData라는 메소드를 활용하면 된다. promise, async/await, callback 모두 사용 가능.

해당 메소드에서 리턴하는 값은 컴포넌트 내에서 this로 접근 가능하다.

---
[Cheat Sheet](https://www.vuemastery.com/pdf/Nuxtjs-Cheat-Sheet.pdf)를 읽어봐도 좋을듯!
