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


## 2강 : Vue 프로젝트 생성 과정 설명 및 서버 실행

$ cd vue3-cli2
$ npm run serve // yarn serve

npm이나 yarn이나 자바스크립트 라이브러리를 로컬에 설치하기 위한 도구.

http://localhost:8080/  
라이브 서버를 들어갈 수 있음

화면은 `public\index.html` 에 있는 html임


## 3강 : Vue 프로젝트 폴더 내용 살펴보기

* package.json
scripts > 프로젝트와 관련된 명령어들 지정  
dependencies > 프로젝트 관련 라이브러리  
devDependencies > 프로젝트 관련 부수적인 라이브러리  
eslintConfig > 자바스크립트 문법 검사 도구  

#### dependencies와 devDependencies의 차이
https://joshua1988.github.io/webpack-guide/build/npm-module-install.html#npm-%EC%A7%80%EC%97%AD-%EC%84%A4%EC%B9%98-%EC%98%B5%EC%85%98-2%EA%B0%80%EC%A7%80

##### 배포용 라이브러리 설치
`npm install jquery --save-prod` == `npm i jquery`
`package.json`의 `dependencies`에 등록된다.
##### 개발용 라이브러리 설치
`npm install jquery --save-dev` == `npm i jquery -D`
`package.json`의 `devDependencies`에 등록된다.

- 개발할 때만 사용하고 배포할 때는 빠져도 좋은 라이브러리의 예시
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
