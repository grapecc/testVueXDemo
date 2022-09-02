# testVueXDemo
learn about Vuex 



## 关于 组件之间数据共享的方式

   父传子 **v-bind 属性绑定**

   子传父 **v-on 事件绑定**

  兄弟之间数据共享  **EevetBus**

-  **$on**   接收数据的那种组件
- **$emit**  发送数据的那个组件

Vuex定义

   vuex是实现组件全局状态管理的一种机制，可以方便实现组件之间的数据共享

一般情况下，只有组件之间共享的数据，才有必要存储到vuex中；对于组件中的私有数据，依旧存储在组件自身的data中即可

###  Vuex的基本使用

#### 1.安装vuex依赖包

```
 npm install vuex --save
```

#### 2.导入vuex包

```
import Vuex form 'vuex'
Vue.use(Vuex)
```

#### 3.创建store 对象

```
new Vuex.Store({
  // state 中存放的全局共享变量
  state:{ count: 0 }
})
```

#### 4.奖store对象挂在到vue实例中

```
new Vue({
 el:'#app',
 render: h => h(app),
 router,
 store
})
```



