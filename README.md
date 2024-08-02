# study log_001

1. vue 설치

https://v2.ko.vuejs.org/v2/guide

3. 선언적 레더링

DOM에서 데이터를 선언적으로 렌더링 가능
```
<div id="app">
  {{ message }}
</div>
```
```
var app = new Vue({
  el: '#app',
  data: {
    message: '안녕하세요 Vue!'
  }
})
```
데이터와 DOM이 연결되며, 모든 것이 반응형으로 된다.
> 테스트방법 : 콘솔창에 app.message 입력

VUE 앱은 단일 DOM요소에 연결되어 DOM 요소를 완전히 제어. HTML은 엔트리 포인트일뿐, 다른 모든 것은 새롭게 생성된 Vue 인스턴스 내에서 발생

4. 엘리먼트 속성 바인딩
```
<div id="app-2">
  <span v-bind:title="message">
    내 위에 잠시 마우스를 올리면 동적으로 바인딩 된 title을 볼 수 있습니다!
  </span>
</div>
```
 
