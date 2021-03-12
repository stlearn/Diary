>## 生命周期
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

