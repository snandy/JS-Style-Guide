# JDC 前端 JavaScript 代码规范

## <a name='table-of-contents'>内容列表</a>

  1. [文件](#jsFile)
  1. [缩进](#indent)
  1. [对象](#objects)
  1. [数组](#arrays)
  1. [字符串](#strings)
  1. [属性](#properties)
  1. [变量](#variables)
  1. [条件表达式和等号](#conditionals)
  1. [语句](#blocks)
  1. [函数](#functions)
  1. [类型转换](#type-casting--coercion)



## <a name='jsFile'>文件</a>

  - JavaScript 文件使用无 BOM 的 UTF-8 编码。

  > 为什么? UTF-8 编码具有更广泛的适应性。BOM 在使用程序或工具处理文件时可能造成不必要的干扰，比如Mac系统中的<a href="http://www.cnblogs.com/snandy/p/4424970.html" target="_blank">换行符问题</a>。



## <a name='indent'>缩进</a>

  - 使用 4 个空格。

    ```javascript
    // bad
    function fn() {
    ∙∙var name;
    }
    // good
    function fn() {
    ∙∙∙∙var name;
    }
    ```
    
  - 每个独立语句结束后必须换行。
  
    ```javascript
    // bad
    user.setCode(1); user.setName('admin'); user.setPwd('123456');

    // good
    user.setCode(1);
    user.setName('admin');
    user.setPwd('123456');
    ```
    
  - `if`、 `else`、 `switch`、 `case`、 `for`、 `while` 和 `:` 后1个空格。

    ```javascript
    // bad
    if(a > b) {

    }
    // good
    if (a > b) {

    }

    // bad
    for(var i = 0; i < 5; i++) {
        // ...
    }
    // good
    for (var i = 0; i < 5; i++) {
        // ...
    }
    ```

  - 赋值语句两边各 1 个空格

    ```javascript
    // bad
    name='John';

    // good
    name = 'John';
    ```  

  - 两元运算符（`==`, `>`, `<`等）两边各 1 个空格。

    ```javascript
    // bad
    if (a==b) {

    }

    // good
    if (a == b) {

    }
    ```    

  - 函数参数之间 1 个空格。

    ```javascript
    // bad
    function ajax(url,param,success) {
        // ...
    }

    // good
    function ajax(url, param, success) {
        // ...
    }
    ```

  - 左大括号前 1 个空格。

    ```javascript
    // bad
    function ajax(url, param, success){
        // ...
    }
    if (a > b){

    }

    // good
    function ajax(url, param, success) {
        // ...
    }
    if (a > b) {

    }
    ```

  - 一元运算符（`++`，`--`）前后不加空格。

    ```javascript
    // bad
    ++ sum;
    total --;

    // good
    ++sum;
    total--;
    ```
    
  - 语句始终使用分号结尾，`for`、 `function`、 `if`、 `switch`、 `try`、 `while` 除外，不要依赖于引擎隐式插入。

    ```javascript
    // bad
    function fn() {
        // ...
    };
    // good
    function fn() {
        // ...
    }

    // bad
    for (var i = 0; i < 5; i++) {
        // ...
    };
    // good
    for (var i = 0; i < 5; i++) {
        // ...
    }
    ```
    
  - 不要将逗号放前面。

    ```javascript
    // bad
    var hero = {
        firstName: 'Bob'
      , lastName: 'Parr'
      , heroName: 'Mr. Incredible'
      , superPower: 'strength'
    };

    // good
    var hero = {
      firstName: 'Bob',
      lastName: 'Parr',
      heroName: 'Mr. Incredible',
      superPower: 'strength'
    };

    ```

  - 起首的大括号跟在关键字的后面，且大括号前留有一个空格。

    ```javascript
    // bad
    if (a > b)
    {
        // ...
    }
    // good
    if (a > b) {
        // ...
    }

    // bad
    function test(){
        console.log('test');
    }
    // good
    function test() {
        console.log('test');
    }

    // bad
    dog.set('attr',{
        age: '1 year',
        breed: 'Bernese Mountain Dog'
    });
    // good
    dog.set('attr', {
        age: '1 year',
        breed: 'Bernese Mountain Dog'
    });
    ```

  - 数组成员以逗号分隔，逗号后加 1 个空格。

    ```javascript
    // bad
    var arr = [1,2,3,4];

    // good
    var arr = [1, 2, 3, 4];
    ```
    
  - 小括号作为函数调用时函数名与左小括号之间没有空格。

    ```javascript
    // bad
    func ();

    // good
    func();
    ```

  - 小括号作为强制运算符时左括号前加 1 个空格。

    ```javascript
    // bad
    return(x + y);

    // good
    return (x + y);
    ```
    
  - 行的长度不应超过80个字符，如果超过应当在运算符（逗号，加号等）后换行。下一行增加两级缩进（8个空格）。
    
    ```javascript
    // bad
    doSomething(argument1, argument2, argument3, argument4, argument5);
    doSomething(argument1, argument2, argument3, argument4, 
        argument5);

    // good
    doSomething(argument1, argument2, argument3, argument4, 
            argument5);
    ```

  - 在单行注释符后留一个空格。

    ```javascript
    // bad
    //this is comment


    // good
    // this is comment
    ```

  - 在多行注释的结束符前留一个空格，使星号对齐。
    ```javascript
    // bad
    /*
      this is comment
    */
    
    // good
    /*
       this is comment
     */
    ```

  - 不要把注释写在多行注释的开始符、结束符所在行。
    ```javascript
    // bad
    /* start

    end */
    /*
    here is line 1
    here is line 2
     */    
    
    // good
    /*
       start
       end
     */
    /*
       here is line 1
       here is line 2
     */         
    ```
    
**[返回列表](#table-of-contents)**

## <a name='objects'>对象</a>

  - [2.1](#2.1) <a name='2.1'></a> 使用对象直接量创建对象。

    ```javascript
    // bad
    var item = new Object();

    // good
    var item = {};
    ```

  - [2.2](#2.2) <a name='2.2'></a> 不要使用 [保留字](http://es5.github.io/#x5.4.1) 当 key，IE8 里有 bug， [查看更多](http://www.cnblogs.com/snandy/archive/2011/04/01/2001727.html)。

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

  - [2.3](#2.3) <a name='2.3'></a> 使用可读性更好的同义词来替代保留字。

    ```javascript
    // bad
    var superman = {
      class: 'alien'
    }

    // good
    var superman = {
      type: 'alien'
    }
    ```

**[返回列表](#table-of-contents)**


## <a name='arrays'>数组</a>

  - [3.1](#3.1) <a name='3.1'></a> 使用数组直接量定义数组。

    ```javascript
    // bad
    var items = new Array();

    // good
    var items = [];
    ```

  - [3.2](#3.2) <a name='3.2'></a> 如果你不知道数组的长度，使用 push。

    ```javascript
    var someStack = [];


    // bad
    someStack[someStack.length] = 'abababa';

    // good
    someStack.push('abababa');
    ```

  - [3.3](#3.3) <a name='3.3'></a> 复制数组使用 slice。

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

  - [3.4](#3.4) <a name='3.4'></a> 使用 slice 将[伪数组](http://www.cnblogs.com/snandy/archive/2011/03/12/1981583.html)的对象转成数组。

    ```javascript
    var foo = document.querySelectorAll('.foo');
    var nodes = Array.prototype.slice.call(foo);
    ```

**[返回列表](#table-of-contents)**

## <a name="strings">字符串</a>

  - [4.1](#4.1) <a name='4.1'></a> 使用单引号定义字符串。

    ```javascript
    // bad
    var name = "Capt. Janeway";

    // good
    var name = 'Capt. Janeway';
    ```

  - [4.2](#4.2) <a name='4.2'></a> 超过80个字符的字符串采用加号 `+`， 多行显示。

    ```javascript
    // bad
    var errorMessage = 'This is a super error that was thrown because of Batman. When you stop how Batman had anything to do with this, you would get nowhere fast.';

    // bad
    var errorMessage = 'This is a super error that was thrown because \
    of Batman. When you stop how Batman had anything to do \
    with this, you would get nowhere fast.';

    // good
    var errorMessage = 'This is a super error that was thrown because ' 
            + 'of Batman. When you stop how Batman had anything to do '
            + 'with this, you would get nowhere fast.';
    ```

  - [4.3](#4.3) <a name='4.3'></a> HTML属性使用双引号，即单引号在外层，双引号在内层。

    ```javascript
    // bad
    var html = "<a href='http://www.jd.com'>京东</a>";
    
    // good
    var html = '<a href="http://www.jd.com">京东</a>';
    ```
    
  - [4.4](#4.4) <a name='4.4'></a> 编程时使用 `join` 而不是字符串连接来构建字符串。

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


## <a name="properties">属性</a>

  - [6.1](#6.1) <a name='6.1'></a> 使用点号 `.` 访问对象属性。

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

  - [6.2](#6.2) <a name='6.2'></a> 当使用变量访问属性时使用中括号 `[]`。

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

  - [7.1](#7.1) <a name='7.1'></a> 使用 `var` 来声明变量，否则会产生全局变量，避免污染全局命名空间。

    ```javascript
    // bad
    superPower = new SuperPower();

    // good
    var superPower = new SuperPower();
    ```
    
  - [7.2](#7.2) 命名采用驼峰式，第一个单词小写，之后的单词首字母大写。

    ```javascript
    // bad
    var nickname = 'John';
    var nick_name = 'John';

    // good
    var nickName = 'John';
    ```
    
  - [7.3](#7.3) 常量名全部用大写字母。

    ```javascript
    // bad
    var pi = 3.1415926;

    // good
    var PI = 3.1415926;
    ```


  - [7.4](#7.4) 避免单个字符名，变量名应具有描述意义（计数器除外）。

    ```javascript
    // bad
    function q() {
        // ...stuff...
    }

    // good
    function query() {
        // ..stuff..
    }
    ```

  - 类（构造器）名首字母大写，用名词。

    ```javascript
    // bad
    function person(name, age) {
        this.name = name;
        this.age = age;
    }

    // good
    function Person(name, age) {
        this.name = name;
        this.age = age;
    }
	```    
    
  - [7.2](#7.2) <a name='7.2'></a> 使用多个 `var` 以及新行声明多个变量。

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

  - [7.3](#7.3) <a name='7.3'></a> 就近声明，用时声明，更自然的在视角范围内。

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

  - [7.4](#7.4) <a name='7.4'></a> 最后声明未赋值的变量，当你想引用之前已赋值变量的时候很有用。

    ```javascript
	// bad
	var width;
	var height;
	var $div = $('#nav');
    
	// good
	var $div = $('#nav');
    var width = $div.width();
    var height = $div.height();
    
    ```

  - [7.5](#7.5) <a name='7.5'></a> 变量应先声明后使用，避免 `变量提升` 现象产生。

    ```javascript
	// bad
	function fn() {
        doStaff(width, height);
        var width = $div.width() || 0;
        var height = $div.height() || 0;
	}

	// good
	function fn() {
        var width = $div.width() || 0;
        var height = $div.height() || 0;
        doStaff(width, height);
	}
    ```

  - [7.6](#7.6) <a name='7.6'></a> 分组声明：变量多且有明显相关性时。

    ```javascript
	// bad
	var x, y, z, width, height;

	// good
	var x, y, z;
	var width, height;
    ```
    
  - 前缀参考

    <table>
		<thead>
			<tr><td>前缀</td><td>类型</td><td>示例</td></tr>
		</thead>
		<tbody>
			<tr><td>is, can has</td><td>Boolean</td><td>isPass</td></tr>
			<tr><td>get</td><td>Getter</td><td>getName</td></tr>
			<tr><td>set</td><td>Setter</td><td>setName</td></tr>
			<tr><td>i, j, k</td><td>iterator</td><td></td></tr>
			<tr><td>el</td><td>HTMLElement</td><td>elNav</td></tr>
			<tr><td>$</td><td>jQuery Object</td><td>$nav</td></tr>
		</tbody>
    </table>

**[返回列表](#table-of-contents)**

## <a name="conditionals">条件表达式和等号</a>

  - [8.1](#8.1) <a name='8.1'></a> 严格比较使用  `===`  和  `!==` ，宽松比较使用 `==`  和  `!=`。多数时候请使用`严格比较`。
  - [8.2](#8.2) <a name='8.2'></a> 条件表达式的转换内部执行ES规范里抽象方法的 `ToBoolean`， 遵循以下规则:

    + **对象** 转换为 **true**
    + **Undefined** 转化为 **false**
    + **Null** 转换为 **false**
    + **Boolean** 转换为 **布尔自身的值**
    + **Number** 如果是 **+0, -0, or NaN** 转换为 **false**，其它转换成 **true**
    + **String** 如果是 空字符串 `''` 转换成 **false** , 其它转化成 **true**

    ```javascript
    if ([0]) {
      // true
      // An array is an object, objects evaluate to true
    }
    ```

  - [8.3](#8.3) <a name='8.3'></a> 使用快捷方式。

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
    
    // bad
    if ($nav.length > 0) {
      // ...stuff...
    }
    // good
    if ($nav.length) {
      // ...stuff...
    }
    ```
    
**[返回列表](#table-of-contents)**

## <a name="blocks">语句</a>

  - [9.1](#9.1) <a name='9.1'></a> 所有多行语句的块使用大括号。

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

  - [9.2](#9.2) <a name='9.2'></a> `if` 和 `else` 块, 把 `else` 和第一个块的结束行放在一行。

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

## <a name="functions">函数</a>

  - 函数的长度控制在 50 行以内。

  > 为什么？将过多的逻辑单元混在一个大函数中，难以维护。一个清晰易懂的函数应该完成单一的逻辑单元。复杂的操作应进一步分解，通过函数的调用来体现流程。

  > 不可分割的特定算法逻辑允许例外。

  - 函数的参数控制在 5 个以内，过多参数会导致维护难度增大。

  > 为什么？ 有些函数的参数并非作为算法的输入，而是对算法的某些分支条件判断之用，此类参数建议通过一个JS对象 options 传递。

  > 某些情况下，如使用 AMD/CMD Loader 的 require 加载多个模块时，其 callback 可能会存在较多参数，因此对函数参数的个数不做强制限制。
  
  - [5.1](#5.1) <a name='5.1'></a> 使用函数声明替代函数表达式。

    ```javascript
    // bad
    var foo = function () {
    };

    // good
    function foo() {
    }
    ```

  - [5.2](#5.2) <a name='5.2'></a> 函数表达式。

    ```javascript
    // immediately-invoked function expression (IIFE)
    (function() {
        console.log('Welcome to the Internet. Please follow me.');
    })();
    ```

  - [5.3](#5.3) <a name='5.3'></a> 不要将一个函数定义非函数块内，如 `if` 、 `while` 语句等。虽然浏览器允许这么干，但在各个浏览器中 <a href="http://w3help.org/zh-cn/causes/SJ9002" target="_blank">表现不一致</a>。

    ```javascript
    if (boo) {
        function bar() {alert(1);}    
    } else {
        function bar() {alert(2);}
    }
    ```


  - [5.4](#5.4) <a name='5.4'></a> 参数不要命名为  `arguments`，该名在函数内自动创建。

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

## <a name="type-casting--coercion">类型转换</a>

  - [10.1](#10.1) <a name='10.1'></a> 字符串。

    ```javascript
    //  => this.reviewScore = 9;

    // bad
    var totalScore = this.reviewScore + '';

    // good
    var totalScore = String(this.reviewScore);
    ```

  - [10.2](#10.2) <a name='10.2'></a> 数字使用 `parseInt` 且总是带上类型转换的基数。

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

  - [10.3](#10.3) <a name='10.3'></a> 出于 [性能考虑](http://jsperf.com/coercion-vs-casting/3)， `parseInt` 不能满足要求时，使用位操作符 `>>` 转换，请注释说明。

    ```javascript
    // good
    /**
     * 此处对性能要求较高，不采用 parseInt 转换，使用 >> 会更快.
     */
    var val = inputValue >> 0;
    ```

  - [10.4](#10.4) <a name='10.4'></a> **注意:** 当使用位移操作要小心，数字以 64 位存储，但 `>>` 最大以 32位运算。因此能转换的最大数字是 2,147,483,647。 超过该范畴的会出现错误：

    ```javascript
    2147483647 >> 0 //=> 2147483647
    2147483648 >> 0 //=> -2147483648
    2147483649 >> 0 //=> -2147483647
    ```

  - [10.6](#10.5) <a name='10.5'></a> 布尔。

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
