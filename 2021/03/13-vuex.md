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
   + Mutations
     > + 
   + Actions
     > + 
   + Modules
     > + 
4. 