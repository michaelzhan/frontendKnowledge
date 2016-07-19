# Function.prototype.bind()的使用 #

#### 程度-进阶

#### ES-5

#### 版本限制

IE9+

## 定义

>bind()方法会创建一个新函数，当这个新函数被调用时，它的this值是传递给bind()的第一个参数, 它的参数是bind()的其他参数和其原本的参数. [MDN文档](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Function/bind)

>apply() 方法在指定 this 值和参数（参数以数组或类数组对象的形式存在）的情况下调用某个函数。[MDN文档](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Function/apply)

## 语法

> fun.bind(thisArg[, arg1[, arg2[, ...]]])

### 参数
* thisArg

  当绑定函数被调用时，该参数会作为原函数运行时的 this 指向。当使用new 操作符调用绑定函数时，该参数无效。

* arg1, arg2, ...

  当绑定函数被调用时，这些参数加上绑定函数本身的参数会按照顺序作为原函数运行时的参数。

## 分析

> 使用bind()可以实现无论在什么作用域中调用此函数，函数的this指针一直不变。

## 典型应用场景

    window.color="red";
    var o = {color:"blue"};

    function sayColor(){
      alert(this.color);
    }

    var objectSayColor=sayColor.bind(o);

    sayColor(); //red;
    objectSayColor(); //blue;
