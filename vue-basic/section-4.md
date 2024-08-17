# Vue JS 템플릿 문법

## 1강

### Vue 템플릿 문법(Template Syntax) 소개

https://joshua1988.github.io/vue-camp/vue/template.html

뷰의 템플릿 문법이란 뷰로 화면을 조작하는 방법을 의미합니다.  
템플릿 문법은 크게 **데이터 바인딩**과 **디렉티브**로 나뉩니다.


* 데이터 바인딩

뷰 인스턴스에서 정의한 속성들을 화면에 표시하는 방법.  
가장 기본적인 데이터 바인딩 방식은 콧수염 괄호(Mustache Tag)입니다.

`<div>{{ message }}</div>`
```javascript
Vue.createApp({
    data() {
        return {
            message: 'Hello Vue.js'
        }
    }
});
```

* 디렉티브

디렉티브는 뷰로 화면의 요소를 더 쉽게 조작하기 위한 문법입니다.  
화면 조작에서 자주 사용되는 방식들을 모아 디렉티브 형태로 제공하고 있습니다.

```html
<div>
  Hello <span v-if="show">Vue.js</span>
</div>
```

```javascript
Vue.createApp({
  data() {
    return {
      show: false
    }
  }
})
```

자주 사용되는 디렉티브
* v-bind
* v-on
* v-model


## 2강

### Vue 디렉티브 : v-if, v-show

* v-if 사용법
```html
<div id="app">
    <p v-if="login">로그인 되었습니다.</p>
    <p v-else>로그인 하세요.</p>
    <button v-on:click="loginUser">로그인</button>
</div>
```

```javascript
Vue.createApp({
    data(){
        return {
            login:false
        }
    },
    methods: {
        loginUser(){
            this.login = !this.login;
        }
    }
}).mount("#app");
```

* v-show 사용법
```html
<div id="app">
    <p v-show="login">로그인 되었습니다.</p>
    <button v-on:click="loginUser">로그인</button>
</div>
```

```javascript
Vue.createApp({
    data(){
        return {
            login:false
        }
    },
    methods: {
        loginUser(){
            this.login = !this.login;
        }
    }
}).mount("#app");
```

## 3강

### Vue 데이터 바인딩: id, class, style

* 클래스 바인딩

`<div class="primary">데이터 바인딩 예제</div>`  
이거를 클래스 바인딩 해보자

```html
<div id="app">
    <h1>클래스 바인딩</h1>
    <div :class="textClass">데이터 바인딩 예제</div>
</div>
```
`v-bind:class`는 `:class`로 축약이 가능하다. (Vue3 부터)

```javascript
Vue.createApp({
    data(){
        return {
            textClass: 'primary',
        }
    }
}).mount("#app");
```

* id 바인딩
`<section id="tab1">`  
를 아이디 바인딩 해보자

```html
<section :id="sectionId">   
    반갑습니다.
</section>
```
`:id`는 `v-bind:id`와 동일
```javascript
Vue.createApp({
    data(){
        return {
            sectionId: 'tab1'
        }
    }
}).mount("#app");
```

* style 바인딩

```html
<section :id="sectionId" :style="sectionStyle">  
    반갑습니다.
</section>

<script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>
<script>
    Vue.createApp({
        data(){
            return {
                sectionId: 'tab1',
                sectionStyle: {color:'red'}
            }
        }
    }).mount("#app");
</script>
```