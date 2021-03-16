# flex布局
## containner
> + diaplay:flex;
> + 控制主轴：justify-content:[center,flex-start,flex-end,space-between,space-around,...]
> + 控制交叉轴：align-items:[center,flex-start,flex-end,...]
> + 控制两个轴：algin-content:[center,flex-start,flex-end,...]
> + 控制必要时换行：flex-warp:[warp]
> + flex-direction:[column,raw]  交换主轴和交叉轴

## item
> + flex-shrink:0  表示不能被压缩
> + flex-grow:1 表示会放大填充   可以为不同数字
> + flex-basis:0 放大缩小的基数，会忽略原来设置的初始大小
> algin-self:[center,flex-start,flex-end,...]控制这一项重写父容器定义
> + order:[1,2,3,....]所有item会按照order排序
