# testVueXDemo
learn about Vuex 



## 关于 组件之间数据共享的方式

   父传子 **v-bind 属性绑定**

   子传父 **v-on 事件绑定**

  兄弟之间数据共享  **EevetBus**

-  **$on**   接收数据的那种组件
- **$emit**  发送数据的那个组件

## Vuex定义

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



##### Vuex的核心概念 state

state 提供的唯一公共数据源，所有共享数据要统一放到Store的State中进行存储

```javascript
// 创建 store 数据源 ，提供唯一公共数据  vue2 
const store = new Vuex.Store({
  state:{count:0}
})

// vue 3  写法  位置store/index
import { createStore } from 'vuex'

export default createStore({
  state: {
    count: 0
  },
  getters: {
  },
  mutations: {
  },
  actions: {
  },
  modules: {
  }
})
// 组件访问变量方式 第一种方式
this.$store.state.全局变量名称
注: 在页面中可以省略this
//第二种方式
//从vuex中 按需导入 mapState函数
import { mapState  } from 'vuex'
通过刚才导入的mapState 函数，奖当前组件需要的全局数据，映射为当前组件的computed计算属性
computed:{
  ...mapState(['count'])  ///... 为展开运算符
}
```

案例   数据+1 /-1

```
 <button @click="addNum">+1</button>
 
 // 错误写法   原因是不能直接修改公共变量  不合法行为
  addNum(){ //count ++
      this.$store.state.count++
    }
```
##### Vuex的核心概念 Mutation

Mutation
   Mutation用于变更Store中的数据

1. 只能通过mutation变更Store数据，不可以直接操作Store中的数据
2. 通过这种方式虽然操作起来繁琐一些，但是可以集中监控所有数据的变化

```javascript
// store 文件
export default createStore({
  state: {
    count: 0
  },
  getters: {
  },
  mutations: {
    add(state){
      //变更状态
      state.count++
    }
  },
  actions: {
  },
  modules: {
  }
})

/组件调用
//触发 mutations的第一种方式
addNum(){ //count ++
// this.$store.state.count++  // 完全不合法
this.$store.commit('add') 
}
注只有mutations 才能直接修改state中的变量
```

Mutation 时传参

```javascript
mutations: {
    addN(state, step){
      //变更状态
      state.count += step
    }
  }
```

/// 使用mutations的第二种方式

```javascript
// 1.从vuex 中按需导入mapMutations
import {mapMutations } from 'vuex'

// 2.指定的mutations 函数 ，映射为当前组件的methods函数
 methods: {
    ...mapMutations(['add','addN'])
  }
```

##### Vuex的核心概念 Action

 Action 用于处理异步任务

如果通过异步操作变更数据，必须通过Action，而不能使用Mutation，但是在Action中还是要通过触发Mutation的方式间接变更数据

store.js 

```javascript
 mutations: {
    add(state){
      //变更状态
      // setTimeout(() =>{
      //   state.count++  不推荐
      // },1000)
      state.count++
    }
  },
  actions: {
    addAsync(context){
      setTimeout(()=>{
        context.commit('add') //commit('add')  add 指的是mutations下的方法
      },1000)
    },
    addAsync3(context,step){
      setTimeout(() =>{
        context.commit('addN', step)
      }, 1000)
    }
  },
  
  
 
  ///组件调用
   this.$store.dispatch('addAsync') //addAsync 指actions下的 方法

   this.$store.dispatch('addAsync3',step)
```

/// 使用actions 的第二种方法

```
// 1. 从vuex中按需导入mapActions 函数
import {mapActions } from 'vuex'

methods: {
...mapActions(['subAsync', 'subAsyncN'])
}


//组件调用
this.subAsyncN(step)
```

Vuex的核心概念 Getter

Getter 用于对Store中数据进行加工处理形成新的数据。

 1.Getter可以对Store 中已有的数据加工处理之后形成新的数据，类似于Vue的计算属性。

2.Store 中数据发生变化，Getter的数据可会跟着变化

```
 state: {
    count: 0
  },
  getters: {
    showNum: state => {
      return '当前最新的数量是【'+state.count+'】'
    }
  },
  
  
  //组件使用第一种方式
  $store.getters.showNum 
  //第二种使用方式
  import {mapGetters } from 'vuex'
  
  computed: {
    //count 第二种方法
    ...mapGetters(['showNum'])
  }
```









