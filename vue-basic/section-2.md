# Vue.js 기본 문법과 개념

## 1강

### Vue Instance = Vue Application Instance

인스턴스는 뷰로 개발할 때 필수로 생성해야 하는 코드입니다.

> Vue 인스턴스란?  
> 화면을 개발하기 위해 필수적으로 생성해야 하는 기본 단위  
데이터를 정의하고, DOM 요소에 바인딩하며, 이벤트를 처리하고, 컴포넌트 간 데이터를 전달하는 등의 기능을 한다.

> Component란?  
> 기본 HTML 엘리먼트를 확장하여 재사용 가능한 코드를 캡슐화하는 데 도움이 된다.


#### VUE 인스턴스 생성 방법
```javascript
Vue.createApp({
    data(){
      return {
        message: 'hi'
      }
    }
  }).mount('#app');
```
인스턴스를 만들어서 인스턴스를 다룰 수 있는 화면의 영역을 지정해주어야 함
```html
<div id="app"></div>
```


## 2강

### Vue Methods

인스턴스 안의 속성들을 **컴포넌트 옵션 속성**, **인스턴스 옵션 속성**, **옵션 API** 라고 부른다.


#### count가 1씩 up되는 버튼을 만들거야

```javascript
Vue.createApp({
    data() {                // == data: function() {
        return {
            count: 0
        }
    },
    methods: {
        addCount() {        // == addCount: function(){}
            this.count++;   // this : createApp에 있는 값을 접근하겠다.
        }
    }
}).mount('#app')
```

```html
<div id="app">
    <p>{{ count }}</p>
    <button v-on:click="addCount">+</button> 
</div>
```

버튼을 클릭할때마다 이 method를 실행하라.


**v-on : 이벤트 핸들링** 

* `click="event"` : 클릭했을 때 실행
* `change="event"` : 요소가 변경될 때 실행
* `dbclick="event"` : 더블 클릭했을 때 실행
* `mouseover="event"` : 마우스의 포인트가 요소 위로 올라왔을 때 실행
* `submit="event"` : form이 제출될 때 실행
* `reset="event"` : form이 재설정될 때 실행
* `select="event"` : select 값이 선택되었을 때 실행
* `focus="event"` : 태그에 포거스가 있을 때 실행
* `keyup="event"` : 키보드의 키를 놓았을 때 실행
* `keydown="event"` : 키보드의 키를 눌렀을 때 실행
* `keypress="event"` : 키보드의 키를 눌렀다가 놓았을 때 실행

**v-on** 디렉티브를 사용해서 DOM의 이벤트를 듣고, 트리거가 될 떄 javascript를 실행할 수 있다.


## 3강

### Vue Directive: v-for

v-if, v-else, v-for, v-bind 여러가지 디렉티브가 존재한다.  
UI 개발을 할 때 추가적으로 자바스크립트 코드를 작성하지않고 좀더 간편하게 작성할 수 있도록 디렉티브 문법 제공.

`참고 URL`  

https://vuejs.org/api/built-in-directives.html#v-for  

https://joshua1988.github.io/vue-camp/syntax/methods.html#%E1%84%86%E1%85%A6%E1%84%89%E1%85%A5%E1%84%83%E1%85%B3-%E1%84%8F%E1%85%A9%E1%84%83%E1%85%B3-%E1%84%92%E1%85%A7%E1%86%BC%E1%84%89%E1%85%B5%E1%86%A8  


v-for 디렉티브를 사용하여 배열을 리스트로 랜더링할 수 있습니다.

#### 고전적인 방법
```html
<div id="app">
    <ul>
        <li>{{ items[0] }}</li>
        <li>{{ items[1] }}</li>
        <li>{{ items[2] }}</li>
    </ul>
</div>
```

#### 개선된 방법
```html
<div id="app">
    <ul>
        <li v-for="item in items">{{ item }}</li>
    </ul>
</div>
```

```javascript
Vue.createApp({
    data(){
        return {
            items: ['삼성', '네이버', '인프런']
        }
    }
}).mount('#app');
```
