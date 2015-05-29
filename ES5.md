# JavaScript代码规范
原文: [https://github.com/airbnb/javascript](https://github.com/airbnb/javascript)，依据本人习惯做了部分修改


## <a name='table-of-contents'>内容列表</a>

  1. [类型](#types)
  1. [对象](#objects)
  1. [数组](#arrays)
  1. [字符串](#strings)
  1. [函数](#functions)
  1. [属性](#properties)
  1. [变量](#variables)
  1. [比较和等值运算符](#conditionals)
  1. [块](#blocks)
  1. [类型转换](#type-casting--coercion)
  1. [许可](#license)

## <a name='types'>类型</a>

  - [1.1](#1.1) <a name='1.1'></a> **原始类型**: 直接传值

    + `string`
    + `number`
    + `boolean`
    + `null`
    + `undefined`

    ```javascript
    var foo = 1;
    var bar = foo;

    bar = 9;

    console.log(foo, bar); // => 1, 9
    ```
  - [1.2](#1.2) <a name='1.2'></a> **复合类型**: 传引用

    + `object`
    + `array`
    + `function`

    ```javascript
    var foo = [1, 2];
    var bar = foo;

    bar[0] = 9;

    console.log(foo[0], bar[0]) // => 9, 9
    ```

**[返回列表](#table-of-contents)**


## <a name='Objects'>对象</a>

  - [2.1](#2.1) <a name='2.1'></a> 使用对象直接量创建对象

    ```javascript
    // bad
    var item = new Object();

    // good
    var item = {};
    ```

  - [2.2](#2.2) <a name='2.2'></a> 不要使用 [保留字](http://es5.github.io/#x5.4.1) 当key，IE8里有bug， [查看更多](http://www.cnblogs.com/snandy/archive/2011/04/01/2001727.html)

    ```javascript
    // bad
    var superman = {
      default: { clark: 'kent' },
      private: true
    };

    // good
    var superman = {
      defaults: { clark: 'kent' },
      hidden: true
    };
    ```

  - [2.3](#2.3) <a name='2.3'></a> 使用可读性更好的同义词来替代保留字

    ```javascript
    // bad
    var superman = {
      class: 'alien'
    }

    // bad
    var superman = {
      klass: 'alien'
    }

    // good
    var superman = {
      type: 'alien'
    }
    ```


**[返回列表](#table-of-contents)**

## <a name='Arrays'>数组</a>

  - [3.1](#3.1) <a name='3.1'></a> 使用数组直接量定义数组

    ```javascript
    // bad
    var items = new Array();

    // good
    var items = [];
    ```

  - [3.2](#3.2) <a name='3.2'></a> 如果你不知道数组的长度，使用Array#push

    ```javascript
    var someStack = [];


    // bad
    someStack[someStack.length] = 'abababa';

    // good
    someStack.push('abababa');
    ```

  - [3.3](#3.3) <a name='3.3'></a> 复制数组使用Array#slice

    ```javascript
    // bad
    var len = items.length;
    var itemsCopy = [];

    for (var i = 0; i < len; i++) {
      itemsCopy[i] = items[i]
    }

    // good
    var itemsCopy = items.slice();
    ```

  - [3.4](#3.4) <a name='3.4'></a> 使用Array#slice将[伪数组](http://www.cnblogs.com/snandy/archive/2011/03/12/1981583.html)的对象转成数组

    ```javascript
    var foo = document.querySelectorAll('.foo');
    var nodes = Array.prototype.slice.call(foo);
    ```

**[返回列表](#table-of-contents)**


## <a name="Strings">字符串</a>

  - [4.1](#4.1) <a name='4.1'></a> 使用单引号定义字符串

    ```javascript
    // bad
    var name = "Capt. Janeway";

    // good
    var name = 'Capt. Janeway';
    ```

  - [4.2](#4.2) <a name='4.2'></a> 超过80个字符的字符串采用加号 `+`， 多行显示

    ```javascript
    // bad
    var errorMessage = 'This is a super long error that was thrown because of Batman. When you stop to think about how Batman had anything to do with this, you would get nowhere fast.';

    // bad
    var errorMessage = 'This is a super long error that was thrown because \
    of Batman. When you stop to think about how Batman had anything to do \
    with this, you would get nowhere \
    fast.';

    // good
    var errorMessage = 'This is a super long error that was thrown because ' +
      'of Batman. When you stop to think about how Batman had anything to do ' +
      'with this, you would get nowhere fast.';
    ```

  - [4.3](#4.3) <a name='4.3'></a> 编程时使用 `join` 而不是字符串连接来构建字符串

   ```javascript
    var items;
    var messages;
    var i, length;

    messages = [{
        state: 'success',
        message: 'This one worked.'
    },{
        state: 'success',
        message: 'This one worked as well.'
    },{
        state: 'error',
        message: 'This one did not work.'
    }];

    length = messages.length;

    // bad
    function inbox(messages) {
      items = '<ul>';

      for (i = 0; i < length; i++) {
        items += '<li>' + messages[i].message + '</li>';
      }

      return items + '</ul>';
    }

    // good
    function inbox(messages) {
      items = [];

      for (i = 0; i < length; i++) {
        items[i] = messages[i].message;
      }

      return '<ul><li>' + items.join('</li><li>') + '</li></ul>';
    }
    ```

**[返回列表](#table-of-contents)**


## <a name="Functions">函数</a>

  - [5.1](#5.1) <a name='5.1'></a> 使用函数声明替代函数表达式

    ```javascript
    // bad
    var foo = function () {
    };

    // good
    function foo() {
    }
    ```

  - [5.2](#5.2) <a name='5.2'></a> 函数表达式

    ```javascript
    // immediately-invoked function expression (IIFE)
    (() => {
      console.log('Welcome to the Internet. Please follow me.');
    })();
    ```

  - [5.3](#5.3) <a name='5.3'></a> 不要将一个函数定义非函数块内，如 `if` `while` 语句等。虽然浏览器允许这么干，但在各个浏览器中<a href="http://w3help.org/zh-cn/causes/SJ9002" target="_blank">表现不一致</a>。
  - [5.4](#5.4) <a name='5.4'></a> **注意:** ECMA-262定义把块定义为一组语句，但函数声明不属于语句。 [查看ECMA-262关于此问题](http://www.ecma-international.org/publications/files/ECMA-ST/Ecma-262.pdf#page=97).

    ```javascript
    // bad
    if (currentUser) {
      function test() {
        console.log('Nope.');
      }
    }

    // good
    let test;
    if (currentUser) {
      test = () => {
        console.log('Yup.');
      };
    }
    ```

  - [5.5](#5.5) <a name='5.5'></a> 参数不要命名为  `arguments`，该名在函数内自动创建

    ```javascript
    // bad
    function nope(name, options, arguments) {
      // ...stuff...
    }

    // good
    function yup(name, options, args) {
      // ...stuff...
    }
    ```

**[返回列表](#table-of-contents)**


## <a name="properties">属性</a>

  - [6.1](#6.1) <a name='6.1'></a> 使用点号 `.` 访问对象属性

    ```javascript
    var luke = {
      jedi: true,
      age: 28,
    };

    // bad
    var isJedi = luke['jedi'];

    // good
    var isJedi = luke.jedi;
    ```

  - [6.2](#6.2) <a name='6.2'></a> 当使用变量访问属性时使用中括号

    ```javascript
    var luke = {
      jedi: true,
      age: 28,
    };

    function getProp(prop) {
      return luke[prop];
    }

    var isJedi = getProp('jedi');
    ```

**[返回列表](#table-of-contents)**


## <a name="variables">变量</a>

  - [7.1](#7.1) <a name='7.1'></a> 使用 `var` 来声明变量，否则会产生全局变量，要避免污染全局命名空间

    ```javascript
    // bad
    superPower = new SuperPower();

    // good
    var superPower = new SuperPower();
    ```

  - [7.2](#7.2) <a name='7.2'></a> 使用多个 `var` 以及新行声明多个变量

    ```javascript
    // bad
    var items = getItems(),
        goSportsTeam = true,
        dragonball = 'z';

    // good
    var items = getItems();
    var goSportsTeam = true;
    var dragonball = 'z';
    ```

  - [7.3](#7.3) <a name='7.3'></a> 就近声明，用时声明，更自然的在视角范围内

    ```javascript
    // bad
    var i, len;
    var goSportsTeam = true;
	var dragonball = 'z';
	
	// ...
		
	for (i = 0; i < len; i++) {
		// ...
	}

    // good
    var goSportsTeam = true;
	var dragonball = 'z';
	
	// ...
		
	for (var i = 0, len = arr.length; i < len; i++) {
		// ...
	}
    ```

  - [7.4](#7.4) <a name='7.4'></a> 最后声明未赋值的变量，当你想引用之前已赋值变量的时候很有用

    ```javascript
	// bad
	var len, dragonball;
	var items = getItems();
	var goSportsTeam = true;

	// bad
	var items = getItems();
	var dragonball;
	var goSportsTeam = true;
	var len;

	// good
	var items = getItems();
	var goSportsTeam = true;
	var dragonball, length;
    ```

  - [7.5](#7.5) <a name='7.5'></a> 在作用域顶部（头部）声明变量，避免声明和赋值引起问题

    ```javascript
	// bad
	function() {
	  test();
	  console.log('doing stuff..');
	  // ...
	  var name = getName();
	  if (name === 'test') {
	    return false;
	  }
	  return name;
	}

	// good
	function() {
	  var name = getName();
	  test();
	  console.log('doing stuff..');
	  // ...
	  if (name === 'test') {
	    return false;
	  }
	  return name;
	}

	// bad
	function() {
	  var name = getName();
	  if (!arguments.length) {
	    return false;
	  }
	  return true;
	}

	// good
	function() {
	  if (!arguments.length) {
	    return false;
	  }
	  var name = getName();
	  return true;
	}  
    ```

  - [7.6](#7.6) <a name='7.6'></a> 分组声明：变量多且有明显相关性时

    ```javascript
	// bad
	var x, y, z, width, height;

	// good
	var x, y, z;
	var width, height;
    ```


**[返回列表](#table-of-contents)**


## <a name="conditionals">条件表达式和等号</a>

  - [8.1](#8.1) <a name='8.1'></a> 适当使用  ===  和  !==  以及  ==  和  != 
  - [8.2](#8.2) <a name='8.2'></a> 条件表达式的转换内部执行ES规范里抽象方法的 `ToBoolean`， 遵循以下规则:

    + **对象** 转换为 **true**
    + **Undefined** 转化为 **false**
    + **Null** 转换为 **false**
    + **Booleans** 转换为 **布尔自身的值**
    + **Numbers** 如果是 **+0, -0, or NaN** 转换为 **false**，其它转换成 **true**
    + **Strings** 如果是 空字符串 `''` 转换成 **false** , 其它转化成 **true**

    ```javascript
    if ([0]) {
      // true
      // An array is an object, objects evaluate to true
    }
    ```

  - [8.3](#8.3) <a name='8.3'></a> 使用快捷方式

    ```javascript
    // bad
    if (name !== '') {
      // ...stuff...
    }
    // good
    if (name) {
      // ...stuff...
    }

    // bad
    if (collection.length > 0) {
      // ...stuff...
    }
    // good
    if (collection.length) {
      // ...stuff...
    }
    ```

  - [8.4](#8.4) <a name='8.4'></a> 见 [JavaScript中奇葩的假值](http://www.cnblogs.com/snandy/p/3589517.html)

**[返回列表](#table-of-contents)**


## <a name="blocks">块</a>

  - [9.1](#9.1) <a name='9.1'></a> 所有多行语句的块使用大括号

    ```javascript
    // bad
    if (test)
      return false;

    // good
    if (test) return false;

    // good
    if (test) {
      return false;
    }

    // bad
    function() { return false; }

    // good
    function() {
      return false;
    }
    ```

  - [9.2](#9.2) <a name='9.2'></a> `if` 和 `else` 块, 把 `else` 和第一个块的结束行放在一行

    ```javascript
    // bad
    if (test) {
      thing1();
      thing2();
    }
    else {
      thing3();
    }

    // good
    if (test) {
      thing1();
      thing2();
    } else {
      thing3();
    }
    ```

**[返回列表](#table-of-contents)**

## <a name="type-casting--coercion">类型转换</a>

  - [10.1](#10.1) <a name='10.1'></a> 在语句的开头执行类型转换
  - [10.2](#10.2) <a name='10.2'></a> 字符串

    ```javascript
    //  => this.reviewScore = 9;

    // bad
    var totalScore = this.reviewScore + '';

    // good
    var totalScore = String(this.reviewScore);
    ```

  - [10.3](#10.3) <a name='10.3'></a> 数字使用 `parseInt` 且总是带上类型转换的基数

    ```javascript
    var inputValue = '4';

    // bad
    var val = new Number(inputValue);

    // bad
    var val = +inputValue;

    // bad
    var val = inputValue >> 0;

    // bad
    var val = parseInt(inputValue);

    // good
    var val = Number(inputValue);

    // good
    var val = parseInt(inputValue, 10);
    ```

  - [10.4](#10.4) <a name='10.4'></a> 出于性能考虑， `parseInt` 不能满足要求时，使用位操作符 `>>` 转换，请注释说明。[性能考虑](http://jsperf.com/coercion-vs-casting/3)

    ```javascript
    // good
    /**
     * parseInt was the reason my code was slow.
     * Bitshifting the String to coerce it to a
     * Number made it a lot faster.
     */
    var val = inputValue >> 0;
    ```

  - [10.5](#10.5) <a name='10.5'></a> **注意:** 当使用位移操作要小心， Numbers are represented as [64-bit values](http://es5.github.io/#x3.2.19), but Bitshift operations always return a 32-bit integer ([source](http://es5.github.io/#x11.7)). Bitshift can lead to unexpected behavior for integer values larger than 32 bits. [Discussion](https://github.com/airbnb/javascript/issues/109). Largest signed 32-bit Int is 2,147,483,647:

    ```javascript
    2147483647 >> 0 //=> 2147483647
    2147483648 >> 0 //=> -2147483648
    2147483649 >> 0 //=> -2147483647
    ```

  - [10.6](#10.6) <a name='10.6'></a> 布尔

    ```javascript
    var age = 0;

    // bad
    var hasAge = new Boolean(age);

    // good
    var hasAge = Boolean(age);

    // good
    var hasAge = !!age;
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


