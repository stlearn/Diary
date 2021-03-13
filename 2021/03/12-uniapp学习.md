##  生命周期
>#### 应用生命周期
>>应用生命周期仅可在App.vue中监听，在其它页面监听无效。
>> + onLanch:初始化完成时触发（全局触发一次）
>> + onShow:当启动或者后台进到前台显示
>> + onHide:当 uni-app 从前台进入后台
>> + onError:错误时触发
>> + ......
>### 页面生命周期
>> + onLoad:监听页面加载，其参数为上个页面传递的数据，参数类型为 Object（用于页面传参)
>> + onShow:监听页面显示。页面每次出现在屏幕上都触发，包括从下级页面点返回露出当前页面
>> + onHide:监听页面隐藏
>> + onPullDownRefresh:用户下拉动作，一般用于下拉刷新
>> + onReachBottom:页面滚动到底部的事件（不是scroll-view滚到底），常用于下拉下一页数据。onReachBottom使用注意 可在pages.json里定义具体页面底部的触发距离onReachBottomDistance，比如设为50，那么滚动页面到距离底部50px时，就会触发onReachBottom事件。
>> + 等等
>### 组件生命周期
>> + beforeCreate	在实例初始化之后被调用.		
>> + created	在实例创建完成后被立即调用。		
>> + beforeMount	在挂载开始之前被调用。		
>> + mounted	挂载到实例上去之后调用。详见 注意：此处并不能确定子组件被全部挂载，如果需要子组件完全挂载之后在执行操作可以使用	
>> + beforeUpdate	数据更新时调用，发生在虚拟 DOM 打补丁之前。仅H5平台支持	
>> + updated	由于数据更改导致的虚拟 DOM 重新渲染和打补丁，在这之后会调用该钩子。仅H5平台支持	
>> + beforeDestroy	实例销毁之前调用。在这一步，实例仍然完全可用。	
>> + destroyed	Vue 实例销毁后调用。调用后，Vue 实例指示的所有东西都会解绑定，所有的事件监听器会被移除，所有的子实例也会被销毁。

## 路由
### 路由跳转
> + 使用navigator组件跳转
>  > - 该组件类似HTML中的a组件，但只能跳转本地页面。目标页面必须在pages.json中注册。 
> + 调用API跳转
> > + uni.navigateTo(OBJECT)
> > + 保留当前页面，跳转到应用内的某个页面，使用uni.navigateBack可以返回到原页面。
### 页面栈
> 框架以栈的形式管理当前所有页面， 当发生路由切换的时候，页面栈会发生变化（很好理解）
---

## 生产环境和开发环境
> + uni-app 可通过 process.env.NODE_ENV 判断当前环境是开发环境还是生产环境。一般用于连接测试服务器或生产服务器的动态切换。
----

# 页面样式与布局
## 尺寸单位
> + uni-app 支持的通用 css 单位包括 px、rpx
> + 750rpx就是屏幕的宽度
> vh 视窗高度 1vh就是1%的高度
> vw 视窗宽度
## 样式导入
> + 使用@import语句可以导入外联样式表，@import后跟需要导入的外联样式表的相对路径，用;表示语句结束。
```html
<style>
   @import "../../common/uni.css";

    .uni-card {
        box-shadow: none;
    }
</style>
```
## 全局样式与局部样式
> + 定义在 App.vue 中的样式为全局样式，作用于每一个页面。
> + App.vue 中通过 @import 语句可以导入外联样式，一样作用于每一个面。
> + 在 pages 目录下 的 vue 文件中定义的样式为局部样式，只作用在对应的页面，并会覆盖 App.vue 中相同的选择器。
> 
## 背景图片
+ 支持网络路径
+ 支持base64
+ 不支持本地路径大图
  
```css
 .test2 {
     background-image: url('~@/static/logo.png');
 }
 ```
---
---

##  '<'template/'>' 和 '<'block/'>'
```html
   <template>
    <view>
        <template v-if="test">
            <view>test 为 true 时显示</view>
        </template>
        <template v-else>
            <view>test 为 false 时显示</view>
        </template>
    </view>
    </template>

    <template>
    <view>
        <block v-for="(item,index) in list" :key="index">
            <view>{{item}} - {{index}}</view>
        </block>
    </view>
    </template>
```





