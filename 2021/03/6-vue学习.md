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

###  建议在mounted做AJAX请求

```html
<body>
<div id="vue">
    <div>
        {{info.name}}{{info.age}}
    </div>
</div>


<script src="https://cdn.bootcss.com/vue/2.5.2/vue.min.js"></script>
<script src="https://cdn.bootcdn.net/ajax/libs/axios/0.21.1/axios.min.js"></script>
<script type="text/javascript">
    let v = new Vue({
        el:"#vue",
        data:{
            message:"你好"
        },
        data(){
          return{
              info:{
              }
          }
        },
        mounted() { //钩子函数 链式编程
            axios.get("../data/axios.json").then(Response=>(this.info = Response.data));
        }
    });
</script>
</body>
```

---

## 计算属性（重要）

计算出来的结果，保存在属性中。计算结果缓存。

![image-20210306223900982](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20210306223900982.png)

```html
<body>
<div id="app">
    method时间{{getTime()}}
    computed时间{{getTime_computed}}
</div>

<script src="https://cdn.bootcss.com/vue/2.5.2/vue.min.js"></script>
<script>
    let v = new Vue({
        el:"#app",
        data:{
            message:1
        },
        methods:{
            getTime:function () {
                return Date.now().toString();
            }
        },
        computed:{
            getTime_computed:function () {
                this.message;
                return Date.now().toString();
            }
        }
    });
</script>
</body>
```

---

---

### 内容分发

插槽<slot></slot>

```html
<body>

<div id="app">
    <todo>
        <todo_title slot="t_title" :title="t"></todo_title>
        <todo_item slot="t_item" v-for="i in songs" :item="i"></todo_item>
    </todo>
</div>

<script src="https://cdn.bootcss.com/vue/2.5.2/vue.min.js"></script>
<script type="text/javascript">

    Vue.component("todo",{
        template:"<div>" +
            "<slot name='t_title'></slot>" +
            "<ul>" +
            "<slot name='t_item'></slot>" +
            "</ul>" +
            "</div>"
    });

    Vue.component("todo_title",{
        props:['title'],
        template:"<div>{{title}}</div>"
    });
    
    Vue.component("todo_item",{
        props:['item'],
        template:"<li>{{item}}</li>"
    });

    let v = new Vue({
       el:"#app",
       data:{
           t:"我喜欢的歌",
           songs:["我爱你爱我","白玫瑰","红玫瑰"]
       }
    });
</script>
</body>
```



----

### 自定义事件

![image-20210306233624563](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20210306233624563.png)

```html
<body>

<div id="app">
    <todo>
        <todo_title slot="t_title" :title="t"></todo_title>
        <todo_item slot="t_item" v-for="(i,shu) in songs" :item="i" :index="shu" v-on:re="removeItems(shu)"></todo_item>
    </todo>
</div>

<script src="https://cdn.bootcss.com/vue/2.5.2/vue.min.js"></script>
<script type="text/javascript">

    Vue.component("todo",{
        template:"<div>" +
            "<slot name='t_title'></slot>" +
            "<ul>" +
            "<slot name='t_item'></slot>" +
            "</ul>" +
            "</div>"
    });

    Vue.component("todo_title",{
        props:['title'],
        template:"<div>{{title}}</div>"
    });

    Vue.component("todo_item",{
        props:['item',"index"],
        template:"<li>{{index}}---{{item}}<button @click='remove(index)' >删除</button></li>",
        methods:{
        remove:function (index) {
            alert(index);
            this.$emit("re");
        }
    }
    });

    let v = new Vue({
        el:"#app",
        data:{
            t:"我喜欢的歌",
            songs:["我爱你爱我","白玫瑰","红玫瑰"]
        },
        methods:{
            removeItems:function (index) {
                console.log("删除了"+index+":"+this.songs[index]);
                this.songs.splice(index,1);
            }
        }
    });
</script>
</body>
```























































