# JS 函数的执行时机

### 6 个 6
上面的代码会打印出 6 个 6，这是由函数的执行时机决定的。首先执行 6 遍 for 循环，执行完成后，i 的值已经等于 6。然后，再执行 6 次 setTimeout，所以会打印出 6 个 6

```
let i = 0
for(i = 0; i<6; i++){
  setTimeout(()=>{
    console.log(i)
  },0)
}
```

### 0、1、2、3、4、5

可以使用块级作用域来将索引值绑定到循环的每一次迭代中，确保使用上一个循环迭代结束时的值重新进行赋值，相当于为每一次索引值都创建一个执行环境

```
for(let i = 0; i<6; i++){
  setTimeout(()=>{
    console.log(i)
  },0)
}
```

### IIFE

可以利用IIFE传参和闭包来创建多个执行环境来保存循环时各个状态的索引值。不同参数的函数被调用时，会创建不同的执行环境

```
let i;
for(i = 0; i<6; i++){
  !function (j) {
    setTimeout(()=>{
        console.log(j)
    },0)
  }(i)
}
```