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
v-bind 속성 : 디렉티브
렌더링된 DOM에 특수한 반응형 동작을 한다.
```
<div id="app-2">
  <span v-bind:title="message">
    내 위에 잠시 마우스를 올리면 동적으로 바인딩 된 title을 볼 수 있습니다!
  </span>
</div>
```
```
var app2 = new Vue({
  el: '#app-2',
  data: {
    message: '이 페이지는 ' + new Date() + ' 에 로드 되었습니다'
  }
})
```

5. 조건문 디렉티브
```
<div id="app-3">
  <p v-if="seen">이제 나를 볼 수 있어요</p>
</div>
```
```
var app3 = new Vue({
  el: '#app-3',
  data: {
    seen: true
  }
})
```
app3.seen = false 를 입력하면, 메시지가 사라지는 것을 볼 수 있습니다.
Vue 엘리먼트가 Vue에 삽입/업데이트/제거될 때 자동으로 트랜지션 효과를 적용할 수 있는 강력한 전환 효과 시스템을 제공한다.

6. 반복문 디렉티브
```
<div id="app-4">
  <ol>
    <li v-for="todo in todos">
      {{ todo.text }}
    </li>
  </ol>
</div>
```
```
var app4 = new Vue({
  el: '#app-4',
  data: {
    todos: [
      { text: 'JavaScript 배우기' },
      { text: 'Vue 배우기' },
      { text: '무언가 멋진 것을 만들기' }
    ]
  }
})
```
반복문에 조건 추가하기
```
app4.todos.push({ text: 'New item' })
```

7. 사용자 입력 핸들링
v-on 디렉티브를 사용하여 Vue 인스턴스에서 메소드를 호출하는 이벤트 리스터를 추가할 수 있다.
```
<div id="app-5">
  <p>{{ message }}</p>
  <button v-on:click="reverseMessage">메시지 뒤집기</button>
</div>
```
```
var app5 = new Vue({
  el: '#app-5',
  data: {
    message: '안녕하세요! Vue.js!'
  },
  methods: {
    reverseMessage: function () {
      this.message = this.message.split('').reverse().join('')
    }
  }
})
```
> 결과 : !sj.euV !요세하녕안

