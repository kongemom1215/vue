# Vue Composition API 기초 

## 1강 : Vue Composition API 소개

### Composition?  
https://vuejs.org/guide/extras/composition-api-faq.html

컴포지션은 컴포넌트 코드 재사용성을 높여주는 API 입니다.

컴포지션 API는 옵션을 선언하는 대신 `import`한 함수를 사용하여 Vue 컴포넌트를 작성할 수 있는 API 세트입니다. 
* Reactivity(반응형) API : 예를들어 `ref()` 및 `reactive()`를 사용하여 반응형 상태, 계산된 상태 및 감시자를 직접 생성할 수 있습니다. 
* LifeCycle Hooks : 예를들어 `onMounted()` 및 `onUnmounted()`를 사용하여 컴포넌트 생명주기에 프로그래밍 방식으로 연결할 수 있습니다. 
* 의존성 주입(Dependency Injection) : `provide()` 및 `inject()`를 사용하면 반응형 API를 사용하는 동안 Vue의 의존성 주입 시스템을 활용할 수 있습니다. 

> 컴포지션 API는 Vue3 및 Vue 2.7에 내장된 기능입니다. 

### Why Compositionm API?

* 더 나은 로직 재사용성  
컴포지션의 가장 큰 장점은 컴포저블 함수의 형태로 깔끔하고 효율적인 로직 재사용이 가능하다는 것입니다.

* 보다 유연한 코드 구성  

* 더 나은 타입 추론  

* 더 작은 프로덕션 번들 및 더 적은 오버헤드

### 반응형 기초

* 반응형 상태 선언

`ref()` : 반응형 상태 선언 권장 방법1  

```javascript
import { ref } from 'vue'

const count = ref(0)
```

count의 값을 가져오려면?
```javascript
const count = ref(0)

console.log(count) // { value: 0 }
console.log(count.value) // 0

count.value++
console.log(count.value) // 1
```

컴포넌트 템플릿의 ref에 액세스하려면, 컴포넌트의 setup() 함수에서 선언하고 반환합니다.
```javascript
import { ref } from 'vue'

export default {
  // `setup`은 Composition API 전용 특수 후크입니다.
  setup() {
    const count = ref(0)

    // ref를 템플릿에 노출
    return {
      count
    }
  }
}
```
```html
<div>{{ count }}</div>
```
템플릿에서 ref를 사용할 때 .value를 추가할 필요가 없었습니다.

이벤트 핸들러에서 직접 참조를 변경할 수도 있습니다:
```html
<button @click="count++">
  {{ count }}
</button>
```

메서드로 이벤트를 만드려면?
```javascript
import { ref } from 'vue'

export default {
  setup() {
    const count = ref(0)

    function increment() {
      // JavaScript 에서 .value 는 필요합니다.
      count.value++
    }

    // 함수를 노출하는 것도 잊지 마세요.
    return {
      count,
      increment
    }
  }
}
```
```html
<button @click="increment">
  {{ count }}
</button>
```


### <script setup>  
setup()을 통해 상태와 메서드를 수동으로 노출하는 것은 장황할 수 있습니다. 다행히 **단일 파일 컴포넌트(SFC)**를 사용하면 피할 수 있습니다. `<script setup>`으로 사용법을 단순화할 수 있습니다:

```javascript
<script setup>
import { ref } from 'vue'

const count = ref(0)

function increment() {
  count.value++
}
</script>

<template>
  <button @click="increment">
    {{ count }}
  </button>
</template>
```

### Why Refs?

템플릿에서 ref를 사용하고 나중에 ref의 값을 변경하면, Vue는 자동으로 이 변경을 감지하고 DOM을 적절하게 업데이트합니다. 이는 의존성 추적 기반의 반응형 시스템으로 가능합니다. 컴포넌트가 처음 렌더링될 때, Vue는 렌더링 과정에서 사용된 모든 ref를 **추적**합니다. 나중에 ref가 변경되면, 이를 추적하는 컴포넌트에 대해 재렌더링을 **트리거**합니다.


## 2강 : Vue Composition API 배경과 오해

Composition이 어떻게 자리를 잡게되었는지.

> 참고 URL : https://github.com/vuejs/rfcs/pull/42
> rfc : request for comment  
> 라이브러리의 방향성을 논의할때.. 라이브러리의 변경점을 공유 

react hook에서 영감을 받아서 composition API를 만든듯?

* Vue와 React의 차이?  
**Vue.js**는 반응성을 기반으로 데이터가 변했을 때 화면을 변화시키는 것  
**React**는 state 변했을 떄 component 코드를 재실행시키면서 전체 화면 랜더링.


## 3강 : Vue Composition API 기본

`setup()` : ref라는 API를 사용해서 변수를 선언할 수 있음. 

* 함수 표현식
```javascript
const changeMessage = () => {
    message.value = 'Hi';
}
```

> 함수 표현식 vs 함수 선언문 : https://joshua1988.github.io/web-development/javascript/function-expressions-vs-declarations/

함수 표현식의 장점?  
호이스팅에 영향을 받지 않는다.


## 4강 : 컴포지션 API 기본 코드 작성

```javascript
<template>
  <div>
    <p>{{ message }}</p>
    <button @click="changeMessage">change</button>
  </div>
</template>

setup(){
    const message = ref('hello');

    // method
    const changeMessage = () => {
        message.value = 'hi';
    };

    return { message, changeMessage };
}
```

ref로 변수 선언, method 선언(변수 값을 바꿀 때는 .value 사용), return 문


## 4강 : Vue Composition API 장점

> Vue2에서 Vue3랑 바뀐점은? https://joshua1988.github.io/web-development/vuejs/vue3-coming/

1. 정확한 타입이 추론된다.

2. 로직을 재사용할 수 있다.  
따로 js파일에 method를 선언하고 가져와서 쓰는 방법 :)
* 디스트럭션 문법
src\hooks\userMessage.js
```javascript
import { ref } from "vue";

function useMessage() {
    const message = ref('hello');

    // method
    const changeMessage = () => {
    message.value = 'hi';
    };

    return { message, changeMessage };
}

export { useMessage }
```

src\App.vue
```javascript
import { ref } from 'vue';
import { useMessage } from './hooks/useMessage'
  
  export default {
    setup(){
      const { message, changeMessage } = useMessage();

      return { message, changeMessage };
    }
  }
```


## 5강 : Vue Composition API 단점

1. 로직을 보기위해서 다른 컴포넌트 파일을 열어보는 비용

추천하는 건, 역할별로 분리 시키는 건 괜찮은데, 기본적으로 옵션 API로 구현하면 중형급 애플리케이션 구축 가능  
실무에서는 컴포지션으로 쪼개고 컴포넌트 설계만 잘하면 좋다. 가급적이면 간결한 코드에서는 setup() API를 사용하지 않는 걸 추천. 

동일한 코드가 반복되는 경우에는 하나의 파일에서 나머지 컴포넌트에 뿌릴수 있는 모듈화는 좋다.

2. setup()을 쓰게 되었을 때, computed(), watch().. 등 많은 API에 대한 사용법을 알아야 한다.

3. setup안에 많은 코드들이 들어가게 되면 데이터, 메소드에 대한 혼동이 올것임.