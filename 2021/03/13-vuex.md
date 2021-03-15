# <strong>vuex</strong>
1. ## 下载安装
   ```shell
   npm install vuex --save
   ```
2. ## 引入定义并注入根组件及所有组件
   ```javascript
    import Vue from 'vue'
    import Vuex from 'vuex'
    //声明使用
    Vue.use(Vuex)

    //定义一个store
    const store = new Vuex.Store({
        state: {
            count: 0
        },
        mutations: {
            increment (state) {
                state.count++
            }
        }
    })

    new Vue({
        el: '#app',
        //全局注册
        store: store
    })


    //在其他组件中这样使用
    this.$store.commit('increment');
    console.log(this.$store.state.count);
   ```
3. ## 核心概念
   + state
     > + 单一状态树
     >>Vuex 使用单一状态树——是的，用一个对象就包含了全部的应用层级状态。至此它便作为一个“唯一数据源 ”而存在。这也意味着，每个应用将仅仅包含一个 store 实例。单一状态树让我们能够直接地定位任一特定的状态片段，在调试的过程中也能轻易地取得整个当前应用状态的快照。
     > + 在 Vue 组件中获得 Vuex 状态
     >> 上面的全局注册加上计算属性
     >>```javascript
     >>computed: {
     >>    count () {
     >>        return this.$store.state.count
     >>    }
     >>}
     >> ```
     > + mapState
     >>```javascript
     >>import { mapState } from 'vuex'
     >>export default{
     >>    computed:mapState(["count"]);
     >>}
     >>```
     > + 对象展开运算符
     >>mapState 函数返回的是一个对象.
     >>可以用...对象展开运算符
     >>```javascript
     >>export default{
     >>    computed:{
     >>    ...mapState(["count",'name']);
     >>    }
     >>}
     >>```
   + Getter
     > + 可以对store中的数据进行处理
     >>```javascript
     >>    const store = new Vuex.Store({
     >>      state:{
     >>          todo:[
     >>          {name:"高云飞",age:22},
     >>          {name:"王五",age:21},
     >>          {name:"张三",age:34},
     >>          {name:"李四",age:33}
     >>          ]
     >>      },
     >>      getters:{
     >>          getOld:(state,getters)=>{
     >>             return getters.getOldThan(30)
     >>          },
     >>          getOldThan:state=>(age)=>{
     >>             return state.todo.filter(todo=>todo.age>age)
     >>          }
     >>      }
     >>    });
     >>console.log(store.getters.getOld);
     >>console.log(store.getters.getOldThan(20));
     >>```
     >+ mapGetters
     >>```javascript
     >>//引入
     >>import { mapState, mapGetters } from "vuex";
     >>
     >>computed: {
     >>    ...mapState(["id", "name"]),
     >>    ...mapGetters(["getOld", "getOldThan"]),
     >>}
     >>//使用
     >>console.log(this.getOld);
     >>console.log(this.getOldThan(21));
     >>```
   + Mutations(转变，变异，变化)(处理同步)
     >```javascript
     >mutations:{
     >   increment(state){
     >      state.count++ 
     >  } 
     >}
     >```
     > + 更改store中状态的唯一途径就是提交mutation。每个 mutation 都有一个字符串的 事件类型 (type) 和 一个 回调函数 (handler)。要唤醒一个 mutation handler，你需要以相应的 type 调用 store.commit 方法：
     >`store.commit('type');`
     > + 提交载荷（Payload）
     >>+ 你可以向 store.commit 传入额外的参数，即 mutation 的 载荷（payload）： 
     >>```javascript
     >>mutations:{
     >>   increment(state){
     >>      state.count++ 
     >>  } 
     >>}
     >>//使用
     >>store.commit('increment',10);
     >>```
     >> + 大多数时候载荷应该是一个对象。
     >>```javascript
     >> mutations: {
     >>    increment (state, payload) {
     >>        state.count += payload.amount
     >>    }
     >> }
     >> store.commit('increment', {
     >>    amount: 10
     >>    }) 
     >>```
     >> + 对象风格的提交
     >>```javascript
     >>store.commit({
     >>    type:'increment',
     >>    amount:10
     >>});
     >>```
     > + Mutation 需遵守 Vue 的响应规则
     >> + 最好提前在你的 store 中初始化好所有所需属性。
     >> + 当需要在对象上添加新属性时，你应该              
     >> `state.obj = { ...state.obj, newProp: 123 }`
     > + Mutation 必须是同步函数(一条重要的准则)
     > + 在组件中提交mutation
     >>1. `this.$store.commit('type')`
     >>2. 使用mapMutations辅助函数
     >>```javascript
     >>import { mapMutations } from 'vuex'
     >>
     >>export default {
     >>  // ...
     >>  methods: {
     >>    ...mapMutations([
     >>      'increment', // 将 `this.increment()` 映射为 `this.    $store.commit('increment')`
     >>
     >>      // `mapMutations` 也支持载荷：
     >>      'incrementBy' // 将 `this.incrementBy(amount)` 映射    为 `this.$store.commit('incrementBy', amount)`
     >>    ]),
     >>    ...mapMutations({
     >>      add: 'increment' // 将 `this.add()` 映射为 `this.  $store.commit('increment')`
     >>    })
     >>  }
     >>}
     >>```
   + Actions(处理异步)
     > + Action类似以mutation,但是有以下不同：
     >> + Action提交的是mutation，而不是直接改变状态
     >> + Action可以包含任意异步操作
     > + 例子
     >>```javascript
     >> actions: {
     >>    increment (context) {
     >>      context.commit('increment')
     >>    }
     >>  }
     >>//参数解构简化代码
     >> actions: {
     >>   increment ({ commit }) {
     >>     commit('increment')
     >>   }
     >> }
     >>```
     > + 分发Action
     >>Action 通过 store.dispatch 方法触发：
     >>`store.dispatch('increment')`
     > + Actions 支持同样的载荷方式和对象方式进行分发
     >>```javascript
     >>// 以载荷形式分发
     >>store.dispatch('incrementAsync', {
     >>  amount: 10
     >>})
     >>
     >>// 以对象形式分发
     >>store.dispatch({
     >>  type: 'incrementAsync',
     >>  amount: 10
     >>})
     >>```
     >+ 在组件中分发Action
     >>`this.$store.dispatch('xxx')`
     >>
     >>或者使用mapActions辅助函数
     > + 组合Action
     >>store.dispatch 可以处理被触发的 action 的处理函数返回的 Promise，并且 store.dispatch 仍旧返回 Promise：
     >>```javascript
     >>actions: {
     >>  actionA ({ commit }) {
     >>    return new Promise((resolve, reject) => {
     >>      setTimeout(() => {
     >>        commit('someMutation')
     >>        resolve()
     >>      }, 1000)
     >>    })
     >>  }
     >>}
     >>//可以这样使用
     >>store.dispatch('actionA').then(() => {
     >>  // ...
     >>})
     >>
     >>//还可以在Action中使用
     >>actions: {
     >>  // ...
     >>  actionB ({ dispatch, commit }) {
     >>    return dispatch('actionA').then(() => {
     >>      commit('someOtherMutation')
     >>    })
     >>  }
     >>}
     >>
     >>// 假设 getData() 和 getOtherData() 返回的是Promise
     >>
     >>//如果我们利用 async / await (opens new window)，我们可以如下组合 action：
     >>actions: {
     >>  async actionA ({ commit }) {
     >>    commit('gotData', await getData())
     >>  },
     >>  async actionB ({ dispatch, commit }) {
     >>    await dispatch('actionA') // 等待 actionA完成
     >>    commit('gotOtherData', await getOtherData     >>())
     >>  }
     >>}
     >>```
     >>一个 store.dispatch 在不同模块中可以触发多个 action 函数。在这种情况下，只有当所有触发函数完成后，返回的 Promise 才会执行。
   + Modules
     > + 由于使用单一状态树，应用的所有状态会集中到一个比较大的对象。当应用变得非常复杂时，store 对象就有可能变得相当臃肿。为了解决以上问题，Vuex 允许我们将 store 分割成模块（module）。每个模块拥有自己的 state、mutation、action、getter、甚至是嵌套子模块——从上至下进行同样方式的分割：
     >>```javascript
     >>const moduleA = {
     >>  state: () => ({ ... }),
     >>  mutations: { ... },
     >>  actions: { ... },
     >>  getters: { ... }
     >>}
     >>
     >>const moduleB = {
     >>  state: () => ({ ... }),
     >>  mutations: { ... },
     >>  actions: { ... }
     >>}
     >>
     >>const store = new Vuex.Store({
     >>  modules: {
     >>    a: moduleA,
     >>    b: moduleB
     >>  }
     >>})
     >>
     >>store.state.a // -> moduleA 的状态
     >>store.state.b // -> moduleB 的状态
     >>```
4. ## 进阶概念
   ### 严格模式
   >开启严格模式，仅需在创建 store 的时候传入 strict: true：
   >>```javascript
   >>const store = new Vuex.Store({
   >>  // ...
   >>  strict: process.env.NODE_ENV !== 'production'
   >>})
   >>```
   >在严格模式下，无论何时发生了状态变更且不是由 mutation 函数引起的，将会抛出错误。
   >不要在发布环境下启用严格模式！严格模式会深度监测状态树来检测不合规的状态变更——请确保在发布环境下关闭严格模式，以避免性能损失。

   ### 表单处理
   > + 创建一个本地变量进行v-model作为mutation的桥梁参数（麻烦）
   > + 创建一个method内部进行mutation的commit
   > + 使用双向绑定的计算属性（清晰明了但是麻烦）
   >>`<input v-model="message">`
   >>```javascript
   >>computed: {
   >>  message: {
   >>    get () {
   >>      return this.$store.state.obj.message
   >>    },
   >>    set (value) {
   >>      this.$store.commit('updateMessage', value)
   >>    }
   >>  }
   >>}
   >>```
  ### 测试
  ### 热重载
  ### 插件