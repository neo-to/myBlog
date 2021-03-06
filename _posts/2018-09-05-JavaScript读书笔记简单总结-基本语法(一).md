---
layout:     post
title:      javaScript读书笔记-基本语法
subtitle:   javaScript读书笔记-基本语法
date:       2018-09-05
author:     limantang
header-img: img/post-bg-ios9-web.jpg
catalog: true
tags:
    - JavaScript
---
# 语句

js代码一行一行执行,一般情况下每一行就是一个语句,
例如这个赋值语句 var a = 1 + 3;
首先使用定义了变量a,然后将1 + 3的结果赋值给a,1 + 3叫做表达式,语句和表达式的主要区别是:
语句是为了进行某种操作,一般情况下不需要返回值,表达式就是为了得到一个值,一定会返回一个值,凡是预期得到一个值得地方都可以使用表达式
最常见的就是等号的右边
# 变量

变量就是对一个值得具名引用,也就是给一个变量起一个见名知意的名字,然后引用这个值

```javascript
    var a = 1;
    //等价于
    var a;
    a = 1
```
如果只是声明而没有赋值,则这个值就是undefined

```javascript
    var a;
    //a ---> undefined
```

如果没有写var命令,而是直接进行了赋值操作也是可以创建变量的

```javascript
    a = 1;
    //或者
    function fn() {
        a = 1
    }
    fn();
    //  a--->1
```

这两种都可以创建一个变量a,但是最大的缺点就是会创建一个全局变量,
不要用这样的写法,其他人不想维护这么睿智的代码


一个变量未经声明就直接使用报错

```javascript
console.log(a)  //  ---> error
```
此方式不同于var命令的直接赋值,两者完全不同

js是动态类型,对类型是没有限制的

```javascript
    var a = 1;
    a = 'b'
    //  a ---> b 
```

如果声明了一个已经存在的变量,而后又重复声明了第二次是无效的

```javascript
    var a = 1;
    var a;
    //  a---> 1
```

## 变量提升

js引擎的工作方式是先解析代码,获取所有的变量,然后在执行,这就会造成声明的变量会被提升到代码的顶部
这就是变量提升...

```javascript
    console.log(a)  //  a--->undefined  
    var a = 1;
```

此方式并不会报错,因为变量提升了,等价于下面的这种写法

```javascript
    var a;
    console.log(a)
    a = 1
```

除此之外还有函数声明的提升

```javascript
    fn();   //  --->函数fn执行了
    function fn() {
    console.log('函数fn执行了')
    }
    //  等价于
    function fn() {
    console.log('函数fn执行了')
    }
    fn()    //  --->函数fn执行了
```

函数提升的另外一种情况,不同于上面的情况

```javascript
    fn()    //  error
    var fn = function(){
    console.log('函数fn执行了')
}
```

此写法会报错,虽然变量会提升,但是具体的赋值语句并不会提升,所以当fn执行时fn还是undefined

# 标识符

js对大小敏感 A不用于a(目前我所接触过的编程语言都会对大小写敏感...)
标识符命名规则还是很简单的:
标识符的首个必须是$(美元符)或者_(下划线)或者英文字母或者其他语言的文字(比如中文)
除了首个以外的部分可以用字母, 其他语言的文字, 数字, _, $

```javascript
    a   //ok
    _a  //ok
    $a  //ok
    1a  //error
    我是标识符   //  ok
    a-  //  error
```

# 注释

两种注释
    1. //    被注释的代码
    2. /** 被注释的代码 */

# 区块

ES5里面,在{}当中使用var命令声明一个变量并不能构成区块

```javascript
    {
        var a = 1
    }
    a   //  a--->1
```

# 条件控制语句

if...else   if...else if

```javascript
    if(表达式) {
        //表达式为真的话执行的语句
    } else {
        //表达式为假的话执行的语句
    }
    
    if(表达式1) {
        //  表达式1为真执行的语句
    } else if(表达式2) {
        //  表达式2为真执行的语句
    }
    
    if(表达式1) {
        //表达式1为真执行的语句
    } else if(表达式2) {
        //表达式2为真执行的语句
    } else {
        //  表达式1和表达式2都为假执行的语句
    }
```

switch语句-->多层if...else if语句可以转化为switch语句

```javascript
    switch(fruit) {
        case 'apple':
        //...
        break
        case 'banana':
        //...
        break
        default:
        //...
    }
```

break语句必须要写上如果你想要到达你想要的效果,也可以不写不会报错,
但是假如符合了第一个条件不会退出switch语句还是会继续向下执行,直到符合条件并且遇到break语句或者一直执行到最后遇到default,
其中case的部分可以填写表达式如: case 1 + 1:
其中switch后面的表达式和case后面的表达式比较时是采用的===而不是==所以不会发生类型转化,这点要注意

三元表达式 条件 ? 表达式 : 表达式   这也是js种唯一一个三元运算符

```javascript
    true ? console.log('true') : console.log('false');
    //  ---> true
    false ? console.log('true') : console.log('false');
    //  ---> false
    // 条件部分可以填写表达式,最后会被转换为布尔值
```

三元运算符在很多场合可以代替if...else..
但是有些情况if...else...并不能满足要求
因为if...else...是个语句并没有返回值,而三目运算符最后返回的是一个值,因为后面的两个元素是表达式一定会返回一个值

```javascript
    console.log(true ? 'true' : 'false')
    //  如果想要用if...else...代替括号里面的内容就要改变整个代码的写法了...
```
for循环语句

```javascript
    for(var i = 0; i < 3; i++) {
    console.log(i)
    }
    //等价于
    var i;
    for(i = 1; i < 3; i++) {
    console.log(i)
    }
    //第一步:首先判断i是否小于3,如果满足条件,执行内部的语句,然后执行第二步,否则执行第三步
    //第二步:i++之后执行第一步
    //第三步:退出循环
    
    //  需要注意的是当i 等于 2时满足条件,执行完语句之后还会执行第二步,执行完毕之后i 等于 3,又进入判断语句,不满足条件,然后执行第三步退出循环,此时i 等于 3
    //  这也是著名的前端面试题打印for循环5个5的一个考点
    
    for(;;){
        //  死循环
    }
    ```
    
    ``while循环语句
    ``
    
    ```javascript
    //  while其实完全和for循环相互转化
    //  就拿上面的for循环来说,可以用while改写
    var i = 0;
    while(i < 3) {
        console.log(i)
        i++
    }
    //  这个时候就可以完全按照代码的顺序来理解了
    //  1,首选判断条件,如果满足则执行代码块
    //  2,然后i++
    //  3,继续判断条件如果不满足条件就退出循环,如果还是满足那就继续从第一步继续判断...
    
    //  退出循环之后i还是等于3
```

do while循环,此语句和while的唯一区别就是,它会先执行一次代码无论条件是真是假块然后再去判断,除此之外没有任何区别

```javascript
    var i = 0;
    do {
    console.log(i)
    i++
    }
    while(i < 3)
```

break和continue 语句都可以起到跳转作用改变代码原有的执行顺序

```javascript
    //  break的含义是终止循环break(终止循环后不会再在判断条件语句)
    //  continue的含义是终止本次循环,开始下次循环
    for(var i = 0; i < 10; i++) {
        console.log(i);
        if (i === 5) {
            break;
        }
    }
    for(var i = 0; i < 10; i++) {
        if (i === 5) {
            break;
        }
        console.log(i);
    }
    //  可以感受一下上面两种写法的不同(是完完全全的退出了循环哦)
    for(var i = 0;i < 10; i++) {
        console.log(i);
        if(i === 5) {
            continue;
        }
    }
    for(var i = 0;i < 10; i++) {
        if(i === 5) {
            continue;
        }
        console.log(i);
    }
    //  感受一下上面的两种写法(如果将循环内部的判断条件写在执行语句的后面其实不会有任何作用)
```






































