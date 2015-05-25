# JavaScript代码风格

## <a name='table-of-contents'>内容列表</a>

  1. [缩进](#indent)
  1. [分号](#semicolon)
  1. [引号](#quotation-marks)
  1. [大括号](#curly-brackets)
  1. [中括号](#square-brackets)
  1. [小括号](#parenthese)
  1. [对象属性](#attribute)
  1. [变量声明](#variable-declaration)
  1. [注释](#comment)

## <a name='indent'>缩进</a>

  - [1.1](#1.1) <a name='1.1'></a> if, else, switch, case, for, while和冒号后1个空格

  - [1.2](#1.2) <a name='1.2'></a> 赋值语句两边各1个空格

  - [1.3](#1.3) <a name='1.3'></a> 两元运算符（==, >, <等）两边各1个空格

  - [1.4](#1.4) <a name='1.4'></a> 函数参数之间1个空格

  - [1.5](#1.5) <a name='1.5'></a> 左大括号前1个空格

  - [1.6](#1.6) <a name='1.6'></a> 一行一条语句，语句行之间2个空格缩进，不使用Tab

  - [1.7](#1.5) <a name='1.7'></a> 一元运算符（++，--）前后不加空格



**[返回列表](#table-of-contents)**

## <a name='semicolon'>分号</a>

  - 语句始终使用分号结尾，for, function, if, switch, try, while 除外，不要依赖于引擎隐式插入。

    ```javascript
    // bad
    function fn() {
      //…
    };
    // good
    function fn() {
      //…
    }

    // bad
    for (var i = 0; i < 5; i++) {
      //…
    };
    // good
    for (var i = 0; i < 5; i++) {
      //…
    }
    ```

**[返回列表](#table-of-contents)**

## <a name='quotation-marks'>引号</a>

  - [3.1](#3.1) <a name='3.1'></a> 引号多用来定义字符串，始终使用单引号

    ```javascript
    // bad
    var name = "John";

    // good
    var name = 'John';
    ```

  - [3.2](#3.2) <a name='3.2'></a> HTML属性使用双引号，即单引号在外层，双引号在内层

    ```javascript
    // bad
    var html = “<a href=’http://www.jd.com’>京东</a>”;

    // good
    var html = ‘<a href=”http://www.jd.com”>京东</a>’;
    ```

**[返回列表](#table-of-contents)**

## <a name='curly-brackets'>大括号</a>

  - 起首的大括号跟在关键字的后面，且留有一个空格。

    ```javascript
    // bad
    if (a > b)
    {
      //…
    }
    // good
    if (a > b) {
      //…
    }

    ```

**[返回列表](#table-of-contents)**

## <a name='square-brackets'>中括号</a>

  - [5.1](#5.1) <a name='5.1'></a> 定义数组，成员以逗号分隔，逗号后加1个空格

    ```javascript
    // bad
    var arr = [1,2,3,4];

    // good
    var arr = [1, 2, 3, 4];
    ```

  - [5.2](#5.2) <a name='5.2'></a> 取对象属性用点号，非标准属性才使用中括号

    ```javascript
    var obj = {name: 'John'};

    // bad
	var name = obj[‘name’];

    // good
    var name = obj.name;
    ```


**[返回首页](#table-of-contents)**

## <a name="parenthese">小括号</a>

  - [6.1](#6.1) <a name='6.1'></a> 作为函数调用时函数名与左小括号之间没有空格

    ```javascript
    // bad
    func ();

    // good
    func();
    ```

  - [6.2](#6.2) <a name='6.2'></a> 作为强制运算符时左括号前加1个空格

    ```javascript
    // bad
    const errorMessage = 'This is a super long error that was thrown because of Batman. When you stop to think about how Batman had anything to do with this, you would get nowhere fast.';

    // bad
    return(x + y);

    // good
    return (x + y);
    ```

**[返回列表](#table-of-contents)**


## <a name="attribute">对象属性</a>

  - 不加引号，除非一些特殊关键字或非合法标识符。

    ```javascript
    // bad
    var obj = {
      'name': 'John',
      'age': 30
    }

    // good
    var obj = {
      name: 'John',
      age: 30
    }
    ```

**[返回列表](#table-of-contents)**

## <a name="variable-declaration">变量命名</a>

  - [8.1](#8.1) <a name='8.1'></a> 当需要使用函数表达式（或匿名函数）时，应使用箭头函数

  > 为什么？ 箭头函数的上下文通常是你想要的， 另外它很简洁。

    ```javascript
    // bad
    [1, 2, 3].map(function (x) {
      return x * x;
    });

    // good
    [1, 2, 3].map((x) => {
      return x * x;
    });
    ```

  - [8.2](#8.2) <a name='8.2'></a> 如函数在一行且只有一个参数，可以省略括号和圆括号，并使用隐式返回。否则，加括号，括号，并使用`返回`声明。

  > 为什么？语法糖，它可读性更好，且可以把多个函数链接在一起.

  > 为什么不？ 当返回一个对象时不要这么干。

    ```javascript
    // good
    [1, 2, 3].map(x => x * x);

    // good
    [1, 2, 3].reduce((total, n) => {
      return total + n;
    }, 0);
    ```

**[返回首页](#table-of-contents)**


## <a name="comment">注释</a>

  - [9.1](#9.1) <a name='9.1'></a> 使用class定义类，避免使用函数及其原型

    ```javascript
    // bad
    function Queue(contents = []) {
      this._queue = [...contents];
    }
    Queue.prototype.pop = function() {
      const value = this._queue[0];
      this._queue.splice(0, 1);
      return value;
    }


    // good
    class Queue {
      constructor(contents = []) {
        this._queue = [...contents];
      }
      pop() {
        const value = this._queue[0];
        this._queue.splice(0, 1);
        return value;
      }
    }
    ```

  - [9.2](#9.2) <a name='9.2'></a> 使用extends实现继承

    ```javascript
    // bad
    const inherits = require('inherits');
    function PeekableQueue(contents) {
      Queue.apply(this, contents);
    }
    inherits(PeekableQueue, Queue);
    PeekableQueue.prototype.peek = function() {
      return this._queue[0];
    }

    // good
    class PeekableQueue extends Queue {
      peek() {
        return this._queue[0];
      }
    }
    ```

**[返回列表](#table-of-contents)**



## License

The MIT License (MIT)

Copyright (c) 2015 snandy

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.

**[返回列表](#table-of-contents)**

# };

