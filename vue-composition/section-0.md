# Vue Composition API 기초 

## 1강 : Vue Composition API 소개

* Composition?  
https://vuejs.org/guide/extras/composition-api-faq.html

컴포지션 API는 옵션을 선언하는 대신 `import`한 함수를 사용하여 Vue 컴포넌트를 작성할 수 있는 API 세트입니다. 
* Reactivity(반응형) API : 예를들어 `ref()` 및 `reactive()`를 사용하여 반응형 상태, 계산된 상태 및 감시자를 직접 생성할 수 있습니다. 
* LifeCycle Hooks : 예를들어 `onMounted()` 및 `onUnmounted()`를 사용하여 컴포넌트 생명주기에 프로그래밍 방식으로 연결할 수 있습니다. 
* 의존성 주입(Dependency Injection) : `provide()` 및 `inject()`를 사용하면 반응형 API를 사용하는 동안 Vue의 의존성 주입 시스템을 활용할 수 있습니다. 

컴포지션 API는 Vue3 및 Vue 2.7에 내장된 기능입니다. 