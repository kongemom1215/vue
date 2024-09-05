## Vue LifeCycle 이해

Vue 인스턴스나 컴포넌트가 생성될 때, 미리 사전에 정의된 몇 단계의 과정을 거치게 되는데 이를 *라이프사이클*이라합니다.  
다시말해, Vue 인스턴스가 생성된 후 우리 눈에 보여지고, 사라지기까지의 단계를 일컫는 말입니다.  

> Vue 인스턴스는 크게 create되고 DOM에 부착(mount)되고, update되며, destroy 되는 4가지 과정을 거치게 됩니다.  

Vue 는 각각의 단계에서 Hook을 걸 수 있도록 API를 제공한다.  
: `beforeCreate, created, beforeMount, mounted, beforeUpdate, updated, beforeDestroy, destroyed`  

`beforeCreate`  
Vue 인스턴스가 초기화 된 직후  
컴포넌트가 DOM에 추가되기 전 (data, methods에 접근 불가능)  

`created`  
data에 직접 접근 가능. 하지만 아직 DOM에 추가되지 않은 상태   

`beforeMount`  
DOM에 부착되기 직전.  
템플릿을 렌더링한 상태로, 가상 DOM이 생성되어있으나 실제 DOM에 부착되지는 않은 상태  

`mounted`  
가상 DOM의 내용이 실제 DOM에 부착되고 난 이후에 실행  

`beforeUpdate`  
data값이 변하면서 DOM에 변화를 적용을 시켜야 할 때가 있는데, 그 직전에 호출되는 것. 

`updated`  
가상 DOM을 렌더링 하고 실제 DOM이 변경된 이후에 호출  

`beforeDestroy`  
해당 인스턴스가 해체되기 직전  
아직 해체되기 이전이므로, 인스턴스는 완전하게 작동하기 때문에 모든 속성에 접근이 가능합니다. 이 단계에서는 이벤트 리스너를 해제하는 등 인스턴스가 사라지기 전에 해야할 일들을 처리하면 됩니다.
 
`destroyed`  
인스턴스가 해체되고 난 직후에 destroyed훅이 호출됩니다.  
해체가 끝난 이후기 때문에, 인스턴스의 속성에 접근할 수 없습니다.  
또한 하위 Vue 인스턴스 역시 삭제됩니다.
