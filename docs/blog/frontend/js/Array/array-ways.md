
# 数组、对象、字符串常见方法

数组，对象，字符串在实现业务逻辑时常常遇到增加，替换 ，删除，截取的要求，为了方便工作中提高工作效率和防止忘记，写了数组，对象，字符串中常用的方法和针对性应用场景。

### 数组
删除数组的某一项或某几项: `array.splice(i,1)`
> 场景：返回的数据中如果返回的是空对象或者空字符串 删除该对象或者删除该字符串
```
//第一种：数组包对象
let arr = [{id:1,name:'amy'},{},{},{},{}];
//第二种：数组包空字符串
let newArr = ['amy','','','',''];
//封装无论是空对象还是空字符串
function DelEmptyObj(temp){
  temp.forEach((item,index)=>{
    //知识点 下面对象中有讲解 判断是否是空对象obj
    if(JSON.stringify(item) == '{}' || item == ''){
      item.splice(index,1);
    }
  })
  retuen temp;
}
//调用函数
DelEmptyObj(arr); // [{id:1,name:'amy'}]
DelEmptyObj(newArr); // ['amy']
```

### 对象

**判断是否是空对象**

> + 判断json字符串是不是'{}'
>
> ```
> let obj = {};
> function verify(obj){
> if(JSON.stringify(obj) == '{}'){
> return true;
> }
> }
> verify(obj);
> ```
>
> + es6新增方法 Object.keys(obj).length 或者 
>
>   ```
>   Object.value(obj).length
>   let obj = {};
>   function change1(arg1){
>   console.log(Object.keys(arg1)); // []
>   if(Object.keys(arg1).length != 0){
>      return true;
>   }
>   }
>   function change2(arg2){
>   console.log(Object.values(arg2)); // []
>   if(Object.values(arg2).length != 0){
>      return true;
>   }
>   }
>   change1(obj1);
>   change2(obj2);
>       
>   ```
**2.判断对象中是否存在某属性**

```
方法一：通过把对象通过keys()转化为数组.indexOf(str)
let obj = {name:'amy',age:18};
console.log(Object.keys(obj).indexOf('amy'));  //true

```

```
方法二：in 
console.log('amy' in obj)  //true
```

```
方法三:hasOwnProperty
console.log(obj.hasOwnProperty('amy'))  //true
```



## 字符串