# Vue JS 핵심 동작  원리

## 1강

### proxy

기존 객체의 동작을 감시하고 제어할 수 있다.

```javascript
<div id="app"></div>

<script>
    var data = {
        a: 10
    }

    var app = new Proxy(data, {
        get(){
            console.log('값 접근')
        },
        set(){
            console.log('값 갱신')
        }
    })
</script>
```

여기서 볼 수 있는 점은 
기본 객체 data의 동작을 가로 채고 이를 get,set을 사용해서 객체의 속성 접근과 갱신을 감시

get 트랩은 객체의 속성에 접근할 때마다 호출  
 ex) 콘솔창에  
    `app.a`  
    `app.data`  
    입력하면 `값 접근`이라고 콘솔창에 적재됨  
set트랩은 객체의 속성을 갱신할 때마다 호출  
 ex) 콘솔창에  
    `app.a=20`  
    입력하면 `값 갱신`이라고 콘솔창에 적재됨  

## 2강

### proxy
객체의 기본 동작을 재정의할 수 있다.

### set

```javascript
new Proxy(target, {
  set(target, property, value, receiver) {},
});
```

* target : 대상 객체
* property : 설정할 속성의 이름 또는 symbol
* value : 설정할 속성의 새 값
* receiver : 할당이 지시된 원래 객체입니다. 이것은 일반적으로 프록시 자체입니다.  
그러나 set() 처리기는 프로토타입 체인이나 다양한 다른 방법 등을 통해 간접적으로 호출할 수도 있습니다.


```javascript
<div id="app">
    <!--여기에 뭐가 렌더링 된다.(렌더링 : 화면에 무언가를 표시하는 행위)-->
</div>

<script>
    var data = {
        message: 10
    }
    
    function render(sth) {
        var div = document.querySelector('#app');
        // DOM API : HTML 태그 정보를 접근할 수 있는 기능
        div.innerHTML = sth;
    }

    var app = new Proxy(data, {
        get(){
            console.log('값 접근')
        },
        set(target, prop, value){ // API 스펙 : API 사용 규격
            target[prop] = value; // 객체target의 속성prop 값에 새로운 값value을 넣어준다.
            render(value);
            console.log('값 갱신')
        }
    })
</script>
```

`app.message='hi'`
> hi
라고했을때, 화면은 hi가 뜨게 되고
`data`
> {message:'hi'}
로 변경되어 있음

vue3는 proxy라고 하는 api를 이용해서 화면을 변경한다


## 3강

### Vue 2 & Vue 3   

### Vue reactivity란?

Vue의 장점이라고 하면 Data Binding이 있습니다.
Vue의 데이터 바인딩은 화면에 표시되는 값과 데이터 값이 연결이 되어 서로를 변경시키기 때문에 양방향 데이터 바인딩이라고도 합니다.
그리고 이 양방향 데이터 바인딩이 가능한 이유가 Vue의 Reactivity 시스템 덕분입니다.

1. 모든 컴포턴트 인스턴스는 watcher 인스턴스를 가진다.
2. watcher 인스턴스는 touched된 properties를 기록한다.
3. setter가 트리거가 되면 watcher의 Notify. 컴포넌트가 다시 렌더링 된다.
