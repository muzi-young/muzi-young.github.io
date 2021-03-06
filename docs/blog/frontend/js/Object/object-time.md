
# 探究时间对象的相关问题

## 时间对象Date()

> 创建一个新的`Date`对象的唯一方法就是通过`new`操作符。
>
> ```
> let newDate = new Date();
> ```
>
> **注意**：如果只是作为常规函数调用，而不加new操作符，返回的只是字符串，不是一个时间对象了。

### `Date()`构造函数有四种形式：

> 1.没有参数 `new Date()`
>
> 如果没有提供参数，那么新创建的时间代表当前的时间。
>
> 2.Unix时间戳 `new Date(value)`
>
> value是int类型的，表示自1970年1月1日00:00:00 UTC以来的毫秒数。
>
> 3.时间戳字符串 `new Date(dateString)`
>
> 表示日期的字符串值。

### *`Date()`的方法*

#### *`Date.prototype.getDate()`*

> *`getDate()`*返回一个指定的日期对象为一个月中的具体哪一天

#### *`Date.prototype.getDay()`*

> *`getDay()`*返回一个具体日期中一周的第几天，0 表示星期天。对于某个月中的第几天

#### *`Date.prototype.getFullYear()`*

> *`getFullYear()`* 方法根据本地时间返回指定日期的年份。

#### *`Date.prototype.getMonth()`*

> 返回一个指定的日期对象的月份，为基于0的值（0表示一年中的第一月）,所以需要月份+1

#### *`Date.prototype.getHours()`*

> *`getHours()`* 返回一个指定的日期对象的小时。

#### *`Date.prototype.getMinutes()`*

> *`getMinutes()`*返回一个指定的日期对象的分钟数。

#### *`Date.prototype.getSeconds()`*

> *`getSeconds()`* 返回一个指定的日期对象的秒数。

#### *`Date.prototype.getTime()`*

> *`getTime()`* 将时间转成时间戳

### 时间戳和时间格式的互转

1.时间戳转成时间格式【以'-‘分割的字符串】

- 只取year-Month-Day

```js
function timestampToTime(timestamp,current) {
    if(current){
        //时间戳为10位需*1000，时间戳为13位的话不需乘1000
         var date = new Date(timestamp); 
    }else{
        var date = new Date(timestamp * 1000); 
    }
    var Y = date.getFullYear() + '-';
    var M = (date.getMonth() + 1 < 10 ? '0' + (date.getMonth() + 1) : date.getMonth() + 1) + '-';
    var D = change(date.getDate()) + ' ';
    return Y + M + D;
}
```

- 包括hour-minute-second

  ```js
  function formatDateTime(time) {
      var date = new Date(time);
      var y = date.getFullYear();
      var m = date.getMonth() + 1;
      m = m < 10 ? ('0' + m) : m;
      var d = date.getDate();
      d = d < 10 ? ('0' + d) : d;
      var h = date.getHours();
      h = h < 10 ? ('0' + h) : h;
      var minute = date.getMinutes();
      var second = date.getSeconds();
      minute = minute < 10 ? ('0' + minute) : minute;
      second = second < 10 ? ('0' + second) : second;
      return y + '-' + m + '-' + d+' '+h+':'+minute+':'+second;
  };
  // 调用方法
  formatDateTime(new Date())
  ```

  

2.时间格式转成时间戳

```js
方法1：
new Date().getTime();
方法2：
new Date().valueOf();
方法3：
Date.parse(new Date());
第三种方法只能精确到秒，前两种方法可以精确到毫秒
```

