# Vue JS 소개

## 1강

#### Evan YOU - 2014년에 만들었음.

### Vue.js 란?
* 간단한 화면 UI 개발부터 라우팅, SSR 등의 애플리케이션 레벨의 개발을 지원하는 프레임워크
    * 라우팅 : 페이지간의 이동 
    * SSR : Server Side Rendering, Vue.js로 SSR을 구현할때 Nuxt기술을 사용한다  
        https://joshua1988.github.io/vue-camp/nuxt/ssr.html
* 리액트와 더불어 실무에서 가장 많이 사용되고 있는 프론트엔드 개발 라이브러리
* 리액트에 비해 진입 장벽이 낮고 쉽게 배울 수 있다.
* 개발 생산성이 높고 자바스크립트 지식이 크게 요구되지 않는다.
* 프론트엔드, 백엔드 등 점차 직무적으로 전문화되고 이쓴ㄴ 상황에서 처음 개발을 시작하는 프론트엔드 개발자 또는 백엔드 개발자에게
선호되는 경향.

#### Vue로 개발된 사이트들
https://www.kakaocorp.com/page/<br/>
https://vibe.naver.com/today<br/>
https://programmers.co.kr/<br/>
https://developer.apple.com/documentation<br/>
https://section.cafe.naver.com/ca-fe/home<br/>

#### 사용하고있는 유명 조직
위키미디어 재단, NASA, Apple, Google, Microsoft, GitLab, Zoom, Tencent, Weibo, Bilibili, Kuaishou

## 2강

### VUE2와 VUE3의 차이점
* 라이브러리 내부 로직 재작성 (to-be : typescript 기반으로 작성)
* 주요 개발 도구들 변경<br/>
    예) 뷰 개발자 도구, VSCode 블러그인(as-is: Vetur, to-be: Volar), Vite 기반 프로젝트 생성(as-is: Webpack(프런트엔드 빌드 도구)) 등
* 컴포지션 API, Teleport 등 새로운 문법 지원 
* 리액티비티 시스템 기반 API 변경
* 공식 문서 변경<br/>
https://vuejs.org/guide/introduction.html

## 3강

### VUE 3의 코드 작성 방식

#### 옵션 API
```javascript
<div id="app">{{ message }}</div>

<script>
    Vue.createApp({
        data() {
            return {
                message: 'hi',
            };
        },
    }).mount('#app');
</script>
```
#### Composition API
```javascript
<div id="app">{{ message }}</div>

<script>
    Vue.createApp({
        setup() {
            const message = ref('hi');

            return {
                message
            }
        }
    }).mount('app');
</script>
```

VUE3에서 옵션 API와 컴포지션 API 둘다 작성할 수 있습니다.<br/>
추천 작성 방법은 이제막 시작한건 options 추천. 재활용, 묘듈화를 지향하는 건 Composition.<br/>
일단 객체 형태를 띄는 options를 사용해봥

## 4강

### 개발 환경 구성
- vsCode 다운
- node js 다운 
- cmder 다운 (git, npm 명령어 사용용)
- vsCode 확장 플러그인 설치 <br/>
    : vue vscode snippets, live server, material icon theme, night owl 설치 <br/>
     volar 가 지금은 vue official로 바뀜<br/>
    위 메뉴에서 terminal> new terminal 생성해서 git bash 사용 추천

## 5강

### cdn
Content Delivery Network : 라이브러리 파일을 어딘가에 배포해두고 서버에 올려놓고 우리가 빠르게 접근할 수 있게 링크로 올려 놓은 것

### hello world 해보기 
```javascript
<script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>

<div id="app">
  {{ message }}
</div>

<script>
  // 인스턴스 생성
  Vue.createApp({
    data(){
      return {
        message: 'hi'
      }
    }
  }).mount('#app');
</script>
```

라이브 서버로 열어서 확인  
개발자도구 > vue에서 데이터 값을 볼 수 있음. 편집도 가능.

data의 변화에 따라서 화면의 ui값이 바뀌는 것이 vue에서 추구하는 reactivity라는 개념.
