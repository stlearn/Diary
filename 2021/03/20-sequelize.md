# Sequeize
## 1.事务
+ 非托管事务
  >提交和回滚事务应由用户手动完成(通过调用适当的 Sequelize 方法)
+ 托管事务
  >如果引发任何错误,Sequelize 将自动回滚事务,否则将提交事务. 另外,如果启用了CLS(连续本地存储),则事务回调中的所有查询将自动接收事务对象.
### (1).非托管事务
>例子：
>```javascript
>// 首先,我们开始一个事务并将其保存到变量中
>const t = await sequelize.transaction();
>
>try {
>
>  // 然后,我们进行一些调用以将此事务作为参数传递:
>
>  const user = await User.create({
>    firstName: 'Bart',
>    lastName: 'Simpson'
>  }, { transaction: t });
>
>  await user.addSibling({
>    firstName: 'Lisa',
>    lastName: 'Simpson'
>  }, { transaction: t });
>
>  // 如果执行到此行,且没有引发任何错误.
>  // 我们提交事务.
>  await t.commit();
>
>} catch (error) {
>
>  // 如果执行到达此行,则抛出错误.
>  // 我们回滚事务.
>  await t.rollback();
>}
>```
>非托管事务方法要求你在必要时手动提交和回滚事务.
### (2).托管事务
>托管事务会自动处理提交或回滚事务. 通过将回调传递给 sequelize.transaction 来启动托管事务. 这个回调可以是 async(通常是)的.
> + Sequelize 将自动开始事务并获得事务对象 t
> + 然后,Sequelize 将执行你提供的回调,并在其中传递 t
> + 如果你的回调抛出错误,Sequelize 将自动回滚事务
> + 如果你的回调成功,Sequelize 将自动提交事务
> + 只有这样,sequelize.transaction 调用才会解决：
>   + 解决你的回调的决议
>   + 或者,如果你的回调引发错误,则拒绝并抛出错误
> 示例
>```javascript
>try {
>
>  const result = await sequelize.transaction>(async (t) => {
>
>    const user = await User.create({
>      firstName: 'Abraham',
>      lastName: 'Lincoln'
>    }, { transaction: t });
>
>    await user.setShooter({
>      firstName: 'John',
>      lastName: 'Boothe'
>    }, { transaction: t });
>
>    return user;
>
>  });
>
>  // 如果执行到此行,则表示事务已成功提交,`result`是事务>返回的结果
>  // `result` 就是从事务回调中返回的结果(在这种情况下为 `user`)
>
>} catch (error) {
>
>  // 如果执行到此,则发生错误.
>  // 该事务已由 Sequelize 自动回滚！
>
>}
>```
>注意,t.commit() 和 t.rollback() 没有被直接调用.
### 自动将事务传递给所有查询
> + 在上面的示例中,仍然通过传递 { transaction: t } 作为第二个参数来手动传递事务.
> + 要将事务自动传递给所有查询,你必须安装 cls-hooked (CLS) 模块,并在自己的代码中实例化命名空间：
> 
