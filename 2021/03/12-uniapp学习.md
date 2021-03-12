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
>> + beforeCreate	在实例初始化之后被调用.		
>> + created	在实例创建完成后被立即调用。		
>> + beforeMount	在挂载开始之前被调用。		
>> + mounted	挂载到实例上去之后调用。详见 注意：此处并不能确定子组件被全部挂载，如果需要子组件完全挂载之后在执行操作可以使用	
>> + beforeUpdate	数据更新时调用，发生在虚拟 DOM 打补丁之前。仅H5平台支持	
>> + updated	由于数据更改导致的虚拟 DOM 重新渲染和打补丁，在这之后会调用该钩子。仅H5平台支持	
>> + beforeDestroy	实例销毁之前调用。在这一步，实例仍然完全可用。	
>> + destroyed	Vue 实例销毁后调用。调用后，Vue 实例指示的所有东西都会解绑定，所有的事件监听器会被移除，所有的子实例也会被销毁。