# async/await 错误处理

目前的处理方式是如下

```JavaScript
getDataHandler(){
  getData().then().catch(err=>{
    console.log(err);
    if(err.message===''){
      // ...
    }
  })
}

async getData(){
  let res = null;

  res = await fetchData();
  // ...
  res = await fetchDataTwo();
  // ...
}
```

这么做是利用 `async` 默认返回的是一个 `Promise` 对象这一操作，`catch` 会捕获 `getData` 中的任意报错，做统一处理。若 `getData` 中的接口属于一个功能点，并且是连续调用，也就是 `getData` 中任一接口调用失败则视为失败的情况下，这么做并没有什么问题

另一种处理方式是

```JavaScript
async getData(){
  try {
  let res = null;

  res = await fetchData();
  // ...
  res = await fetchDataTwo();
  // ...
  }catch(err){
    console.log(err);
    if(err.message===''){
      // ...
    }
  }
}
```

这一方式与上一个差不多，只是这样做少去了一个 `Handler` 方法，并且可以让事件直接使用该方法，可以算是上一种方法的改善版本，当然，还有个不太推荐的方式如下

```JavaScript
async getData(){
  let res = null;

  res = await fetchData().catch(err=>{
    console.log(err);
    // ...
  });
  // ...
  res = await fetchDataTwo().catch(err=>{
    console.log(err);
    // ...
  });
  // ...
}
```

每一次的请求都单独进行错误处理，确实是处理了所有的错误，但是让代码较为冗长，接下来的一种应该是类似的

```JavaScript
// 抽离成公共方法
const awaitWrap = (promise) => {
    return promise
        .then(data => [null, data])
        .catch(err => [err, null])
}

async getData(){
  let err  =null;
  let res = null;

  [err,res] = await awaitWrap(fetchData());
  if(err){
    //...
  }
  // ...
  [err,res] = await awaitWrap(fetchDataTwo());
  if(err){
    //...
  }
  // ...
}
```

利用 `Promise` 捕获每一个错误，算上一种方式的升级版
