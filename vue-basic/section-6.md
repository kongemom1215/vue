# Vue 싱글 파일 컴포넌트

## 1강: Vue Single File Component 소개

### 싱글 파일 컴포넌트 

싱글 파일 컴포넌트는 화면의 특정 영역에 대한 HTML, CSS, JS 코드를 한 파일에서 관리하는 방법.  

> 뷰 CLI로 프로젝트를 생성하고 나면 App.vue라는 파일을 확인할 수 있는데, 이처럼 .vue 확장자를 가진 파일을 모두 싱글 파일 컴포넌트라고 한다.

```html
<!-- .vue 파일 구조 -->
<template>
  <!-- html (뷰 컴포넌트의 표현단, 템플릿 문법) -->
</template>

<script>
  // 자바스크립트 (뷰 컴포넌트 내용)
</script>

<style>
  /* CSS (뷰 템플릿의 스타일링) */
</style>
```
> 이게 바로 뷰 싱글 파일 컴포넌트의 형식이다.


### 싱글 파일 컴포넌트의 동작 원리
뷰 로더에 의해 HTML, CSS, JS와 같은 웹 자원으로 분리되어 실행됩니다. 

> 뷰 로더는 웹팩의 로더 종류 중 하나이고, 뷰 CLI 로 프로젝트를 생성하면 기본적으로 설정이 되어 있다.


* 싱글 파일 컴포넌트 명명규칙 : 컴포넌트는 무조건 파스칼 케이스(HelloWorld)로 작성


## 2강 : App 컴포넌트

* import 문법
`import 라이브러리 from '라이브러리이름'` ex) vue  
`import 파일이름 from './파일경로'`  

* 인스턴스 옵션 속성
```javascript
export default {
    name: 'App',
    components: {
        HelloWorld
    }
}
```


## 3강 : 싱글 파일 컴포넌트 코드 작성 팁

* Vue VsCode Snippets 활용  

`vbc` : 싱글 파일 컴포넌트 형식이 만들어짐 (template-script-style)  

`vda` : data() 스니펫 제공

`v-on:click` : `@click`로 축약

```javascript
<template>
  <div>
    {{ message }}
  </div>
  <button @click="showAlert">경고</button>
</template>

<script>
  export default {
    data() {
      return {
        message: 'hi'
      }
    },
    methods:{
      showAlert(){
        alert('hello')
      }
    }
  }
</script>

<style scoped>

</style>
```


## 4강 : Vue 컴포넌트 등록 방법 및 명명 규칙

### 컴포넌트를 등록하고 가져오는 방법

1. components 폴더에 AppHeader.vue 생성

2. App.vue에 AppHeader.vue 추가하기
    1. AppHeader.vue 파일 추가   
    `import AppHeader from './components/AppHeader.vue';`  
    `// import 컴포넌트이름 from '.컴포넌트 경로'`
    2. components에 AppHeader 추가
    ```javascript
     components: {
        AppHeader
    },
    ```
    > // '컴포넌트 이름': 컴포넌트 내용
    > // 'AppHeader': AppHeader
    3. template에 컴포넌트 추가
    ```javascript
    <template>
        <AppHeader></AppHeader>
    </template>
    ```


## 5강 : 싱글파일 컴포넌트의 props, event emit

### App 컴포넌트에서 AppHeader로 props 데이터 전달

1. AppHeader.vue
```javascript
<template>
    <h1>{{ appTitle }}</h1>
</template>

<script>
    export default {
        props: ['appTitle']
    }
</script>
```
App.vue에서 appTitle props를 받아오자

2. App.vue
``` javascript
<template>
  <AppHeader 
    v-bind:appTitle="message">
  </AppHeader>
</template>

export default {
  components: {
    AppHeader
  },
  data() {
    return {
      message: '앱 헤더 컴포넌트'
    }
  }
}
```
appTitle을 상위 컴포넌트의 message에 연결(bind)

### AppHeader의 이벤트를 발생해서 App에서 처리해보자

1. AppHeader.vue
```javascript
<template>
    <h1>{{ appTitle }}</h1>
    <button @click="changeTitle">버튼</button>
</template>

<script>
    export default {
        props: ['appTitle'],
        methods: {
            changeTitle(){
                this.$emit('change');
            }
        }
    }
</script>
```

버튼을 클릭하면 changeTitle 메소드가 실행되고, 상위 컴포넌트에 change로 전달

2. App.vue
```javascript
<template>
  <AppHeader 
    v-bind:appTitle="message" 
    v-on:change="changeMessage">
  </AppHeader>
</template>

export default {
  name: 'App',
  components: {
    AppHeader
  },
  data() {
    return {
      message: '앱 헤더 컴포넌트'
    }
  },
  methods:{
    changeMessage(){
      this.message = '변경됨'
    }
  }
}
```
change랑 bind된 changeMessage 메소드 실행

