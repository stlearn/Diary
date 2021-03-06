# 3-6

#### 今天学习vue.js

---

1. ### CSS预处理器

   less

2. ### Vue-UI  Ice.work

3. #### jQuery

   封装的BOM DOM操作

4. #### Angular.js

   MVC  MVVM(数据双向绑定)

5. ### MVVM

   时间驱动编程方式

   ViewModel 双向数据绑定

---

#### Vue.js就是一个MVVM的实现者

---



## Vue基础语法

- [ ] 判断 v-if v-else-if c-else

- [ ] 循环 v-for=“i in item”

- [ ] 事件绑定 通过v-on:来绑定事件

  ```javascript
  var vm = new Vue({
          el:"#app",
          data:{
              message:"你好"
          },
          methods:{
              sayHi:function (event) {
                  alert(this.message);
              }
          }
      });
  
  ```

---

## Vue数据双向绑定

- [ ] v-model

  ```html
  <body>
  <div id="app">
      <input type="text" v-model = "message">{{message}}
  </div>
  <script src="https://cdn.bootcss.com/vue/2.5.2/vue.min.js"></script>
  <script>
      var vm = new Vue({
          el:"#app",
          data:{
              message:"你好"
          }
      });
  </script>
  </body>
  ```

---

### Vue组件

![image-20210306154413802](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20210306154413802.png)

页头 侧边栏 底部等

```html
<body>
<div id="app">
    <Gao v-for="item in items" v-bind:my="item"></Gao>
</div>

<script src="https://cdn.bootcss.com/vue/2.5.2/vue.min.js"></script>
<script>
    Vue.component("Gao",{
        props:["my"],
        template:'<li>{{my}}</li>'
    });
    let v = new Vue({
        el:"#app",
        data:{
            items:["milk","banana","orange"]
        }
    });
</script>
</body>
```

----

### Axios异步通信

+ jQuery.AJAX 缺点：频繁操作DOM

+ 什么是Axios 发送xhr请求

  ![image-20210306160530306](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20210306160530306.png)

  

  ### vue生命周期

![](https://cn.vuejs.org/images/lifecycle.png)

























































