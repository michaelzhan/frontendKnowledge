# Function.prototype.call()与 Function.prototype.apply()的使用 #


## 定义

>call() 方法在使用一个指定的this值和若干个指定的参数值的前提下调用某个函数或方法. [MDN文档](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Function/call)

>apply() 方法在指定 this 值和参数（参数以数组或类数组对象的形式存在）的情况下调用某个函数。[MDN文档](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Function/apply)

***

## 语法

> fun(arg1[, arg2[, ...]]]) //调用函数,使用当前上文，参数为列表形式

> fun.call(thisArg[, arg1[, arg2[, ...]]]) //调用函数，可指定上下文对象, 参数是列表形式

> fun.apply(thisArg[, argsArray])  //调用函数，可指定上下文对象, 参数以数组形式传入

### 参数
* thisArg

    在fun函数运行时指定的this值。需要注意的是，指定的this值并不一定是该函数执行时真正的this值，如果这个函数处于非严格模式下，则指定为null和undefined的this值会自动指向全局对象(浏览器中就是window对象)，同时值为原始值(数字，字符串，布尔值)的this会指向该原始值的自动包装对象。

* arg1, arg2, ...

    指定的参数列表。

* argsArray

    一个数组或者类数组对象，其中的数组元素将作为单独的参数传给 fun 函数。如果该参数的值为null 或 undefined，则表示不需要传入任何参数。从ECMAScript 5 开始可以使用类数组对象。浏览器兼容性请参阅本文底部内容。

***

## 分析

> 使用call或apply方法的好处在于可以将对象方法和对象解耦。

## 典型应用场景

1. 示例1- 模拟面向对象中的方法继承

    在面向对象思想中，在子类的对象上可以调用父类中定义的方法，此时函数仍然是父类中定义的函数，但执行时的作用域是子类的对象。在JS中，这种语法就正好可以通过call/apply函数来实现:


    function Product(name, price) {
      this.name = name;
      this.price = price;

      if (price < 0) {
        throw RangeError('Cannot create product ' +
                          this.name + ' with a negative price');
      }

      return this;
    }

    function Food(name, price) {
      Product.call(this, name, price);
      this.category = 'food';
    }

    Food.prototype = Object.create(Product.prototype);
    Food.prototype.constructor = Food; // Reset the constructor from Product to Food

    function Toy(name, price) {
      Product.call(this, name, price);
      this.category = 'toy';
    }

    Toy.prototype = Object.create(Product.prototype);
    Toy.prototype.constructor = Toy; // Reset the constructor from Product to Toy

    var cheese = new Food('feta', 5);
    var fun = new Toy('robot', 40);
