## await后面要跟Promise才会等执行完再进到下一步
```javascript

    method:{
        await getList(){
            let l = await list();
            console.log(l);
            console.log("已经完成")
        },
        list(){
            return new Promise((resolve,reject)=>{
                uni.request({
                    url:"xxx/xx/x";
                    method:'GET',
                    success:(res){
                        resolve(res);
                    }   
                });
            });
        }
    }
```