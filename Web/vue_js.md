# Vue.js
  - Component 기반의 웹 프론트용 프레임워크이다.
  - VirtualDOM을 사용하여 렌더링 속도 최적화.
  - 서버사이드 렌더링 지원
  - 템플릿 기반의 구조(기본은 템플릿이지만 JSX를 원하면 사용할 수도 있음)
  - [API 링크](https://kr.vuejs.org/v2/api/)
  
## Instance's life-cycle
  ![Instance's life cycle](https://kr.vuejs.org/images/lifecycle.png)
https://kr.vuejs.org/v2/api/#%EC%98%B5%EC%85%98-%EB%9D%BC%EC%9D%B4%ED%94%84%EC%82%AC%EC%9D%B4%ED%81%B4-%ED%9B%85

### 1. Creation
컴포넌트가 DOM에 추가되기 전의 훅으로, 서버 렌더링에서도 지원된다.
클라이언트/서버 렌더링 모두에서 처리해야 할 일이 있다면 이 단계를 이용하면 된다. 아직 컴포넌트가 DOM에 추가되기 전이기 때문에 돔에 접근하거나 hthis.$el을 사용할 수 없다.

#### beforeCreate
모든 훅 중에서 가장 먼저 실행된다. 아직 data와 events가 셋팅되지 않은 시점이므로 접근하려고 하면 에러가 발생한다.

#### created
data와 events가 활성화되어 접근할 수 있다. 템플릿과 가상의 DOM은 아직 마운트/렌더링 되지 않은 상태이다.

### 2. Mounting
초기 렌더링 직전에 컴포넌트에 직접 접근할 수 있다. 서버렌더링에서는 지원하지 않는다.

#### beforeMount
템플릿과 렌더 함수들이 컴파일 된 후에 첫 렌더링이 일어나기 직전 실행된다. 대부분의 경우에는 사용하지 않는 것이 좋다.

#### mounted
컴포넌트, 템플릿, 렌더링 된 돔에 접근할 수 있다. 모든 하위 컴포넌트가 마운트된 상태를 보장하지는 않는다.
```js
mounted() {
  this.$nextTick(function() {
    // 모든 화면이 렌더링된 후 실행
  })
}
```
![parent/child initialization workflow](https://cdn-images-1.medium.com/max/1600/1*7nxq9WPZrQA_0tj0ultWqw.png)
  
  
### 3. Updating
컴포넌트에서 사용되는 반응형 속성들이 변경되거나 재 렌더링이 발생할 경우 실행된다. 서버렌더링에서는 호출되지 않는다.

#### beforeUpdate
이 훅은 컴포넌트의 데이터가 변하여 업데이트 사이클이 시작될때 실행된다. 정확히는 돔이 재 렌더링되고 패치되기 직전에 실행된다.

#### updated
컴포넌트의 데이터가 변하여 재 렌더링이 일어난 후에 실행된다. 돔 업데이트가 완료된 상태이므로 돔 종속적인 연산을 할 수 있다.

### 4. Destruction
#### beforeDestroy
뷰 인스턴스가 제거되기 직전에 호출된다. 컴포넌트는 원래 모습과 모든 기능을 그대로 가지고 있다. 이벤트 리스터를 제거하거나 reactive subscription을 제거하고자 한다면 이 훅을 사용하면 된다.

#### destroyed
뷰 인스턴스가 제거된 후에 호출된다. 

더 상세한 설명은 [여기](https://medium.com/witinweb/vue-js-%EB%9D%BC%EC%9D%B4%ED%94%84%EC%82%AC%EC%9D%B4%ED%81%B4-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0-7780cdd97dd4)를 참고하자.


## Option/Data
[참고 링크](https://kr.vuejs.org/v2/api/#%EC%98%B5%EC%85%98-%EB%8D%B0%EC%9D%B4%ED%84%B0)
  
## Store
Vuex(Vue.js의 상태 관리 패턴 라이브러리)에서 제공하는 중앙 집중식 저장소이다. 
어플리케이션의 모든 컴포넌트에 대해 한 곳에서 관리하게 된다.
![vuex state flow](https://vuex.vuejs.org/vuex.png)

### 상태
Vuex는 **단일 상태 트리**를 사용한다. 각 어플리케이션마다 하나의 저장소를 가지게 된다.
상태는 `computed`를 통해 가져올 수 있다.
```vue
// ...이하 생략
computed: {
  count() {
    return store.employees.count
  }
}
```
`computed` 내에서 상태를 가져오게 되면, 상태(`store.employees.count`) 값이 변할 경우 계산된 속성이 변경되고 DOM 업데이트가 트리거 된다.

상태 값을 변경하고 싶을 경우 `commit`메소드를 이용한다.
[TODO: READ](https://vuex.vuejs.org/kr/guide/mutations.html)

  
  
  
## Slot
좋은 기능을 알았다. 부모 컴포넌트에서 자식 컴포넌트로 DOM element를 전달할 수 있다.

React에서는 `{{ children }}` 으로 호출할 수 있지만, vue에서는 방법을 못찾고 있어서 템플릿 스트링으로 넘겨주고 있던 도중, slot을 발견!!

```vue
// Parent.vue
<Child>
  <p>부모에서 넘겨준 엘리먼트 입니다.</p>
</Child>
```

```vue
// Child.vue
<p>자식 컴포넌트 입니다.</p>
<slot></slot>
```

렌더링이 되면, 아래와 같을 것이다.
```vue
<p>자식 컴포넌트 입니다.</p>
<p>부모에서 넘겨준 엘리먼트 입니다.</p>
```

[참고 링크](https://kr.vuejs.org/v2/guide/components.html#%EB%8B%A8%EC%9D%BC-%EC%8A%AC%EB%A1%AF)


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

### /plugins
루트 vue.js 어플리케이션이 생성되기 전 실행하고 싶은 js 플러그인을 포함.

### /static
정적 파일 포함. 이 디렉토리 내의 파일에 접근할때에는 루트(/)에 연결

### /store
Vuex store 파일 포함
