# Vue Component 

## 1강

### Vue Component 소개

https://joshua1988.github.io/vue-camp/vue/components.html

![image](https://github.com/user-attachments/assets/5420fac4-7f7e-40ac-8dd9-770ce0b29f5b)


컴포넌트는 화면의 영역을 구분하여 개발할 수 있는 뷰의 기능입니다.  
컴포넌트 기반으로 화면을 개발하게 되면 코드의 재사용성이 올라가고 빠르게 화면을 제작할 수 있습니다.

* 컴포넌트 tree : 트리구조 형태로 형성
* root 컴포넌트 : 최상위 컴포넌트


## 2강

### Vue Component 등록과 표시

* 컴포넌트 등록하기1
```javascript
Vue.createApp({
    // 인스턴스 옵션 속성 = 옵션 api
    components: {
        // '컴포넌트 이름': 컴포넌트 내용
        'app-header': {
            template: '<h1>컴포넌트 등록</h1>'
        }
    }
}).mount('#app');
```

* 컴포넌트 등록하기2
```javascript
// 인스턴스 생성
var app = Vue.createApp();

// 전역 컴포넌트 등록
app.component('app-header', {
  template: '<h1>Header Component</h1>'
});
```

* 컴포넌트 표시하기
```html
<div id="app">
    <app-header></app-header>
</div>
```

## 3강

### Vue Component 통신 방식

https://joshua1988.github.io/vue-camp/vue/components-communication.html  

뷰 컴포넌트는 각각 고유한 데이터 유효 범위를 갖습니다.  
따라서, 컴포넌트 간에 데이터를 주고 받기 위해선 아래와 같은 규칙을 따라야 합니다.

![image](https://github.com/user-attachments/assets/4d01e4ea-97b2-4ebe-a5dc-c1359691f854)

* 상위에서 하위로는 데이터를 내려줌, **프롭스 속성**
* 하위에서 상위로는 이벤트를 올려줌, **이벤트 발생**


## 4강

### Vue Component Props

상위, 하위 컴포넌트 == 부모, 자식 컴포넌트

#### Props 속성
프롭스 속성은 컴포넌트 간에 데이터를 전달할 수 있는 컴포넌트 통신 방법입니다.  
프롭스 속성을 기억할 때는 상위 컴포넌트에서 하위 컴포넌트로 내려보내는 데이터 속성으로 기억하면 쉽습니다.

* 자식 컴포넌트에 props를 전달하기
  
`<app-header v-bind:프롭스이름="상위컴포넌트의 데이터이름"></app-header>`


```html
<div id="app">
    <app-header v-bind:title="appTitle"></app-header>
</div>
```

v-bind를 통해서 상위 컴포넌트의 데이터를 바인딩(연결)시킨다.

```javascript
Vue.createApp({
    data(){
        return {
            appTitle: '프롭스 넘기기'
        }
    },
    components: {
        'app-header': {
            template: '<h1>{{ title }}</h1>',
            props: ['title']
        }
    }
}).mount('#app');
```

* 결과

![image](https://github.com/user-attachments/assets/569fe22c-1f74-4a6c-a11e-6dae1e9493e5)

![image](https://github.com/user-attachments/assets/5e43d044-55fd-450a-89fe-a8249185fc3e)

