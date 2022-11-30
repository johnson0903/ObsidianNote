
## Vue 應用實例

每個 Vue 應用都是透過 `createApp` 凾式創建

```Javascript
import { createApp } from 'vue'

const app = createApp({
  /* 根组件选项 */
})

```


---

## 根元件 (Root Component)

`createApp` 函式內傳入的其實就是一個元件，每個 Vue 應用都需要有 "根元件"，其他元件可作為其子組件。

如果使用 Single-File Component，通常會將根元件寫在另一個檔案中

```Javascript
import { createApp } from 'vue' 
// import the root component App from a single-file component. 
import App from './App.vue' 

const app = createApp(App)
```


---

## 掛載應用

必須呼叫 `mount()` 才會將應用渲染，`mount`方法接受一個**容器**參數，可使用實際的 DOM 元素或 CSS Selector

```html
<div id="app"></div>
```

```Javascript
app.mount('#app')
```


- 注意：mount() 回傳的值是 ==根元件的 instance== 而非 app instance，這邊與 Vue 2 不同的是，若要存取在 `createApp` 時傳入的參數，例如 data、method 等等，不能用 vue.data1、vue.func1 而是須將 回傳的根元件 instance 儲存起來，並從根元件 instance 上存取

```Javascript
import { createApp } from 'vue'

const app = createApp({
  template: '<div>{{ msg }} from template option</div>',
  data(){
    return {
      msg: '123'
    }
  },
  methods: {
    func1(){
      console.log('hi func');
    }
  }
})

const vm = app.mount('#app')

console.log(vm.msg);
vm.func1()

// 下面這樣寫會沒值和出錯
console.log(vm.msg); // undefined
app..func1() // Uncaught TypeError: app.func1 is not a function


```


---

## DOM 中的根元件模板

在沒有使用構建工具時，可以直接在掛載的容器中直接寫模板語法，這也是我們專案中常用的方法之一，透過 Razor view 將 HTML 產生好，再掛載成 Vue 應用

```html
<div id="app">
  <button @click="count++">{{ count }}</button>
</div>
```

```Javascript
import { createApp } from 'vue'

const app = createApp({
  data() {
    return {
      count: 0
    }
  }
})

app.mount('#app')
```


