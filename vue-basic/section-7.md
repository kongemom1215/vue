# Vue.js 최종 프로젝트

## 1강 : 프로젝트 생성 및 로그인 폼 UI 구성

```javascript
<template>
  <form action="">
    <div>
      <label for="userId">ID : </label>
      <input id="userId" type="text" v-model="username">
    </div>
    <div>
      <label for="password">PW : </label>
      <input id="password" type="password" v-model="password">
    </div>
    <button type="submit">로그인</button>
  </form>
</template>

<script>
  export default {
    data() {
      return {
        username: '',
        password: ''
      }
    },
  }
</script>
```

### v-model 동작원리  
https://joshua1988.github.io/web-development/vuejs/v-model-usage/  
사용자의 입력을 받는 UI 요소들에 `v-model`이라는 속성을 사용하면 입력 값이 자동으로 뷰 데이터 속성에 연결 된다.

`v-model` 속성은 `v-bind`, `v-on` 기능의 조합으로 동작한다.
예를들면, 
```javascript
<input v-bind:value="inputText" v-on:input="updateInput">

new Vue({
  data: {
    inputText: ''
  },
  methods: {
    updateInput: function(event) {
      var updatedText = event.target.value;
      this.inputText = updatedText;
    }
  }
})
```

* v-bind 속성은 뷰 인스턴스의 데이터 속성을 해당 HTML 요소에 연결할 때 사용한다.
* v-on 속성은 해당 HTML 요소의 이벤트를 뷰 인스턴스의 로직과 연결할 때 사용한다.
* 사용자 이벤트에 의해 실행된 뷰 메서드(methods) 함수의 첫 번째 인자에는 해당 이벤트(event)가 들어온다.


### v-model 공식 문서
https://vuejs.org/guide/essentials/forms.html


### typescript란?
https://joshua1988.github.io/ts/why-ts.html#%ED%83%80%EC%9E%85%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8%EB%9E%80  

타입스크립트는 자바스크립트에 타입을 부여한 언어입니다. 자바스크립트의 확정된 언어라고 볼 수 있다.  
타입스크립트는 자바스크립트와 달리 브라우저에서 실행하려면 파일을 한번 변환해주어야 한다.  
이 변환 과정을 compile이라 부른다.

> 타입스크립트를 쓰는 이유는?
> 에러의 사전 방지, 코드 가이드 및 자동완성(개발 생산성 향상)


## 2강 : 폼 이벤트 제어 및 서버로 데이터 전송

xhr(Xml Http Request)

* 프론트엔드 개발자가 알아야 하는 HTTP 프로토콜   
https://joshua1988.github.io/web-development/http-part1/

### submit할때마다 새로고침되는 현상 개선

* 방법 1
``` javascript
<template>
  <form action="" @submit="submitForm">
    <div>
      <label for="userId">ID : </label>
      <input id="userId" type="text" v-model="username">
    </div>
    <div>
      <label for="password">PW : </label>
      <input id="password" type="password" v-model="password">
    </div>
    <button type="submit">로그인</button>
  </form>
</template>

...
methods: {
      submitForm(event) {
        event.preventDefault(); // form의 기본적인 동작 막기(submit할때 새로고침하는)
        console.log('제출됨');
      }
    }
...
```

* 방법 2
```javascript
<template>
  <form action="" @submit.prevent="submitForm">
    <div>
      <label for="userId">ID : </label>
      <input id="userId" type="text" v-model="username">
    </div>
    <div>
      <label for="password">PW : </label>
      <input id="password" type="password" v-model="password">
    </div>
    <button type="submit">로그인</button>
  </form>
</template>
```
이러면 이벤트 방지!

### HTTP 통신을 해보자!
axios 다운로드 : https://github.com/axios/axios  
> axios? node.js와 브라우저를 위한 Promise 기반 HTTP 클라이언트

1. axios 설치 
`$ npm install axios`

2. import
`import axios from 'axios';`

3. http 통신
https://jsonplaceholder.typicode.com/  
fake api를 이용해보자.  
```javascript
import axios from 'axios';
export default {
data() {
    return {
    username: '',
    password: ''
    }
},
methods: {
    submitForm() {
        const data={
            username: this.username,
            password: this.password
        };
        axios.post('https://jsonplaceholder.typicode.com/users/', data)
        .then(response => {
            console.log(response)
        });
    }
}
}
```
개발자도구 > 네트워크 창을 통해 확인 가능


## 3강 : Vue Composition API 코드로 변환하기 

컴포지션 API 작성법
```javascript
<template>
  <form action="" @submit.prevent="submitForm">
    <div>
      <label for="userId">ID : </label>
      <input id="userId" type="text" v-model="username">
    </div>
    <div>
      <label for="password">PW : </label>
      <input id="password" type="password" v-model="password">
    </div>
    <button type="submit">로그인</button>
  </form>
</template>

<script>
import axios from 'axios';
import { ref } from 'vue';
export default {
    setup() {
        //data
        var username = ref('');
        var password = ref('');

        //methods
        var submitForm = () => {
        axios.post('https://jsonplaceholder.typicode.com/users/', {
            username: username.value,
            password: password.value
        })
        .then(response => {
            console.log(response)
        });
        }
        
        return { username, password, submitForm }
    },
    methods:{
        logText(){
        console.log(this.username);
        }
    }
}
</script>
```
`return { username, password, submitForm }` 을 해주면 인스턴스 옵션 내에서 재사용할 수 있음