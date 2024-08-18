# VUE CLI : 뷰 프로젝트 생성 도구

## 1강 : Vue CLI 소개 및 설치

VUE CLI(Command Line Interface)는 VUE JS로 프로젝트를 시작할 떄 주로 사용하는 프로젝트 생성 도구  
명령어로 프로젝트를 생성할 수 있어서 많이 사용함

https://cli.vuejs.org/

`npm install -g @vue/cli`  
-g : global

* npm?  
Node Package Manager로, 명령어로 자바스크립트 라이브러리를 설치하고 관리할 수 있는 패키지 매니저입니다.


* NPM 소개 문서 : https://joshua1988.github.io/webpack-guide/build/node-npm.html#node-js%EC%99%80-npm

* NPM 무료 강의 : https://www.inflearn.com/course/lecture?courseSlug=%ED%94%84%EB%9F%B0%ED%8A%B8%EC%97%94%EB%93%9C-%EC%9B%B9%ED%8C%A9&unitId=37371

* npmjs.com  
전세계의 자바스크립트 라이브러리들을 전부 다 관리한다.  
jquery라던지.. 

프로젝트 생성 : `vue create 프로젝트이름`  
> 이 명령어에는 'npm install vue', 'npm install vue core-js' 등 필요한 라이브러리들을 다 들고 오게 되어있다.


## 2강 : Vue 프로젝트 생성 과정 설명 및 서버 실행

$ cd vue3-cli2
$ npm run serve // yarn serve

npm이나 yarn이나 자바스크립트 라이브러리를 로컬에 설치하기 위한 도구.

http://localhost:8080/  
라이브 서버를 들어갈 수 있음

화면은 `public\index.html` 에 있는 html임


## 3강 : Vue 프로젝트 폴더 내용 살펴보기

* package.json  
> scripts > 프로젝트와 관련된 명령어들 지정  
> dependencies > 프로젝트 관련 라이브러리  
> devDependencies > 프로젝트 관련 부수적인 라이브러리  
> eslintConfig > 자바스크립트 문법 검사 도구  

#### dependencies와 devDependencies의 차이
https://joshua1988.github.io/webpack-guide/build/npm-module-install.html#npm-%EC%A7%80%EC%97%AD-%EC%84%A4%EC%B9%98-%EC%98%B5%EC%85%98-2%EA%B0%80%EC%A7%80

##### 배포용 라이브러리 설치
`npm install jquery --save-prod` == `npm i jquery`
`package.json`의 `dependencies`에 등록된다.
##### 개발용 라이브러리 설치
`npm install jquery --save-dev` == `npm i jquery -D`
`package.json`의 `devDependencies`에 등록된다.

* 개발할 때만 사용하고 배포할 때는 빠져도 좋은 라이브러리의 예시
    * `webpack` : 빌드 도구
    * `eslint` : 코드 문법 검사 도구
    * `imagemin` : 이미지 압축 도구

##### 효율을 위한 도구들
https://joshua1988.github.io/web-development/vuejs/boost-productivity/

* `Prettier` : 코드 스타일을 정리해주는 도구. ESLint와 함께 사용한다.
* `ESLint` : 코드 문법 검사기. 세미콜론, 콤파를 붙여주고.. 미리 알려줌으로서 서비스 품질을 높임
* `Vue VSCode Snippets` : VSCode 확장 플러그인. 

* vue.config.js : 뷰 프로젝트 설정 파일  
vue/cli-service  
웹팩에 대한 설정  
ctrl+space로 사용가능한 옵션 확인

* public\index.html  
```html
<div id="app">
    <!-- 이 안에 표시되는 결과물이 Vue CLI로 빌드된 결과물 -->
</div>
```

* src\main.js  
index.html의 스크립트

* Vue CLI의 API 문서  
https://cli.vuejs.org/config/#vue-config-js


## 4강 : 라이브러리, 파일 임포트 방식 설명

```javascript
// 뷰 라이브러리를 들고 옴
import { createApp } from 'vue'  
```
'vue' : 라이브러리  
package.json의 dependencies를 보면 vue 라이브러리를 확인할 수 있다.  
> 이제 cdn으로 가져오지 않아도 된다!

* \node_modules  
를 가보면 라이브러리 목록들을 확인할 수 있다.  

* 인스턴스 생성법
`import { createApp } from 'vue'` 이 말은 `const { createApp } = Vue`와 동일해서  
이제는 `Vue.createApp...`할 필요 없이 `createApp`으로 하면 된다.  

```javascript
// 뷰 파일을 들고 옴
import App from './App.vue'
```
뷰의 싱글 파일 컴포넌트(.vue)

## 5강 : 페이지 로딩 과정 분석

개발자도구 > Network를 통해서 흐름 파악하기

* Vue Loader란?  
https://vue-loader.vuejs.org/  
Vue 구성 요소를 SFC(단일 파일 구성 요소) 라는 형식으로 작성할 수 있는 WebPack용 로더입니다.

```javascript
<template>
  <div class="example">{{ msg }}</div>
</template>

<script>
export default {
  data () {
    return {
      msg: 'Hello world!'
    }
  }
}
</script>

<style>
.example {
  color: red;
}
</style>
```
다음과 같은 멋진 기능이 제공된다.  
    * Vue 구성 요소의 각 부분에 대해 다른 WebPack 로더를 사용할 수 있다. `<template>`


* loader란?  
https://joshua1988.github.io/webpack-guide/concepts/loader.html  
로더는 웹팩이 웹 애플리케이션을 해석할 때 자바스크립트 파일이 아닌 웹 자원(HTML, CSS< Images, font 등)들을 변환할 수 있도록 도와주는 속성

* WebPack 이란?  
https://joshua1988.github.io/webpack-guide/webpack/what-is-webpack.html  
최신 프론트엔드 프레임워크에서 가장 많이 사용되는 Module Bundler입니다.  
모듈 번들러란 웹 애플리케이션을 구성하는 자원(HTML, CSS, Javscript, Images 등)을 모두 각각의 모듈로 보고 이를 조합해서 병합된 하나의 결과물을 만드는 도구를 의미합니다.  

* 모듈이란?  
프로그래밍 관점에서 특정 기능을 갖는 작은 코드 단위  
```javascript
    // math.js
    function sum(a, b) {
    return a + b;
    }

    function substract(a, b) {
    return a - b;
    }

    const pi = 3.14;

    export { sum, substract, pi }
```
이 `math.js` 파일은 아래와 같이 3가지 기능을 갖고 있는 모듈입니다.

1. 두 숫자의 합을 구하는 sum() 함수
2. 두 숫자의 차를 구하는 substract() 함수
3. 원주율 값을 갖는 pi 상수

* WebPack에서의 모듈?
웹팩에서 지칭하는 모듈이라는 개념은 위와 같이 자바스크립트 모듈에만 국한되지 않고 웹 애플리케이션을 구성하는 모든 자원을 의미합니다. 웹 애플리케이션을 제작하려면 HTML, CSS, Javascript, Images, Font 등 많은 파일들이 필요하죠. 이 파일 하나하나가 모두 모듈입니다.

