# ES6代码规范
原文: [https://github.com/airbnb/javascript](https://github.com/airbnb/javascript)，依据本人习惯做了部分修改


## <a name='table-of-contents'>内容列表</a>

  1. [引用](#references)
  1. [对象](#objects)
  1. [数组](#arrays)
  1. [解构](#destructuring)
  1. [字符串](#strings)
  1. [函数](#functions)
  1. [箭头函数](#arrow-functions)
  1. [构造器](#constructors)
  1. [模块](#modules)
  1. [迭代器和生成器](#iterators-and-generators)
  1. [变量](#variables)
  1. [变量提升](#hoisting)
  1. [ES5兼容性](#ecmascript-5-compatibility)
  1. [ES6风格](#ecmascript-6-styles)
  1. [资源](#resources)
  1. [许可](#license)


## <a name='references'>引用</a>

  - [1.1](#1.1) <a name='1.1'></a> 使用关键字 `const` 声明变量，避免使用 `var`。

  > 为什么？这可以确保该变量不能二次赋值，可以减少bug及晦涩代码的。

    ```javascript
    // bad
    var a = 1;
    var b = 2;

    // good
    const a = 1;
    const b = 2;
    ```

  - [1.2](#1.2) <a name='1.2'></a> 如果需要使用可变的引用，使用 `let`，不要使用 `var`。

  > 为什么？ `let` 在函数内具有块级作用域，`var` 没有。

    ```javascript
    // bad
    var count = 1;
    if (true) {
      count += 1;
    }

    // good, use the let.
    let count = 1;
    if (true) {
      count += 1;
    }
    ```

  - [1.3](#1.3) <a name='1.3'></a> 注意 `let` 和 `const` 都具有块级作用域。

    ```javascript
    // const and let only exist in the blocks they are defined in.
    {
      let a = 1;
      const b = 1;
    }
    console.log(a) // ReferenceError
    console.log(b) // ReferenceError
    ```

**[返回列表](#table-of-contents)**

## <a name='objects'>对象</a>

  - [2.1](#2.1) <a name='2.1'></a> 使用简写的属性

    ```javascript
    const lukeSkywalker = 'Luke Skywalker';

    // bad
    const obj = {
      lukeSkywalker: lukeSkywalker
    };

    // good
    const obj = {
      lukeSkywalker
    };
    ```

  - [2.2](#2.2) <a name='2.2'></a> 简写属性放在开头并分组

    ```javascript
    const anakinSkywalker = 'Anakin Skywalker'
    const lukeSkywalker = 'Luke Skywalker'

    // bad
    const obj = {
      episodeOne: 1,
      twoJedisWalkIntoACantina: 2,
      lukeSkywalker,
      episodeThree: 3,
      mayTheFourth: 4,
      anakinSkywalker,
    }

    // good
    const obj = {
      lukeSkywalker,
      anakinSkywalker,
      episodeOne: 1,
      twoJedisWalkIntoACantina: 2,
      episodeThree: 3,
      mayTheFourth: 4,
    }
    ```

**[返回列表](#table-of-contents)**

## <a name='arrays'>数组</a>

  - [3.1](#3.1) <a name='3.1'></a> 使用扩展运算符 `...` 复制数组

    ```javascript
    // bad
    const len = items.length;
    const itemsCopy = [];
    let i;

    for (i = 0; i < len; i++) {
      itemsCopy[i] = items[i];
    }

    // good
    const itemsCopy = [...items]
    ```

  - [3.2](#3.2) <a name='3.2'></a> 使用Array.from将伪数组转成数组

    ```javascript
    const foo = document.querySelectorAll('.foo');
    const nodes = Array.from(foo);
    ```

**[返回列表](#table-of-contents)**

## <a name='destructuring'>解构</a>

  - [4.1](#4.1) <a name='4.1'></a> 使用对象解构

    ```javascript
    // bad
    function getFullName(user) {
      const firstName = user.firstName
      const lastName = user.lastName

      return `${firstName} ${lastName}`
    }

    // good
    function getFullName(obj) {
      const { firstName, lastName } = obj
      return `${firstName} ${lastName}`
    }

    // best
    function getFullName({ firstName, lastName }) {
      return `${firstName} ${lastName}`
    }
    ```

  - [4.2](#4.2) <a name='4.2'></a> 使用数组解构

    ```javascript
    const arr = [1, 2, 3, 4]

    // bad
    const first = arr[0]
    const second = arr[1]

    // good
    const [first, second] = arr
    ```

  - [4.3](#4.3) <a name='4.3'></a> 使用对象解构一次返回多个值。

    ```javascript
    // bad
    function processInput(input) {
      // then a miracle occurs
      return [left, right, top, bottom];
    }

    // the caller needs to think about the order of return data
    const [left, __, top] = processInput(input);

    // good
    function processInput(input) {
      // then a miracle occurs
      return { left, right, top, bottom };
    }

    // the caller selects only the data they need
    const { left, right } = processInput(input);
    ```


**[返回首页](#table-of-contents)**

## <a name="strings">字符串</a>

  - [5.1](#5.1) <a name='5.1'></a> 使用模板替代字符串拼加。

    ```javascript
    // bad
    function sayHi(name) {
      return 'How are you, ' + name + '?';
    }

    // bad
    function sayHi(name) {
      return ['How are you, ', name, '?'].join();
    }

    // good
    function sayHi(name) {
      return `How are you, ${name}?`;
    }
    ```

**[返回列表](#table-of-contents)**


## <a name="functions">函数</a>

  - [6.1](#6.1) <a name='6.1'></a> 使用扩展运算符替代 `arguments`。

  > 为什么？ `...` 具有arguments的所有功能，并且它是一个真正的数组，`arguments` 则是一个伪数组。

    ```javascript
    // bad
    function concatenateAll() {
      const args = Array.prototype.slice.call(arguments);
      return args.join('');
    }

    // good
    function concatenateAll(...args) {
      return args.join('');
    }
    ```

  - [6.2](#6.2) <a name='6.2'></a> 多个参数有默认值时，使用默认参数特性。

    ```javascript
    // really bad
    function handleThings(opts) {
      opts = opts || {};
      // ...
    }

    // still bad
    function handleThings(opts) {
      if (opts === void 0) {
        opts = {};
      }
      // ...
    }

    // good
    function handleThings(opts = {}) {
      // ...
    }
    ```

  - [6.3](#6.3) <a name='6.3'></a> 注意避免默认参数的副作用。

    ```javascript
    var b = 1;
    // bad
    function count(a = b++) {
      console.log(a);
    }
    count();  // 1
    count();  // 2
    count(3); // 3
    count();  // 3
    ```

**[返回列表](#table-of-contents)**

## <a name="arrow-functions">箭头函数</a>

  - [7.1](#7.1) <a name='7.1'></a> 当需要使用函数表达式（或匿名函数）时，应使用箭头函数。

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

  - [7.2](#7.2) <a name='7.2'></a> 如函数在一行且只有一个参数，可以省略括号和圆括号，并使用隐式返回。否则，加括号并使用 `return` 声明。

  > 为什么？语法糖，它可读性更好，且可以把多个函数链接在一起。

    ```javascript
    // good
    [1, 2, 3].map(x => x * x);

    // good
    [1, 2, 3].reduce((total, n) => {
      return total + n;
    }, 0);
    ```

**[返回首页](#table-of-contents)**


## <a name="constructors">构造器</a>

  - [8.1](#8.1) <a name='8.1'></a> 使用 `class` 定义类，避免使用函数及其原型。

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

  - [8.2](#8.2) <a name='8.2'></a> 使用 `extends` 实现继承。

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

  - [8.3](#8.3) <a name='8.3'></a> 方法内可以返回 `this` 实现链式调用。

    ```javascript
    // bad
    Jedi.prototype.jump = function() {
      this.jumping = true;
      return true;
    };

    Jedi.prototype.setHeight = function(height) {
      this.height = height;
    };

    const luke = new Jedi();
    luke.jump(); // => true
    luke.setHeight(20); // => undefined

    // good
    class Jedi {
      jump() {
        this.jumping = true;
        return this;
      }

      setHeight(height) {
        this.height = height;
        return this;
      }
    }

    const luke = new Jedi();

    luke.jump().setHeight(20);
    ```

  - [8.4](#8.4) <a name='8.4'></a> 可以重写类的toString方法，只要确保它可用且无副作用。

    ```javascript
    class Jedi {
      contructor(options = {}) {
        this.name = options.name || 'no name';
      }

      getName() {
        return this.name;
      }

      toString() {
        return 'Jedi - ${this.getName()}';
      }
    }
    ```

**[返回列表](#table-of-contents)**


## <a name="modules">模块</a>

  - [9.1](#9.1) <a name='9.1'></a> 经常使用 (`import`/`export`) 在非标准的模块系统中，你可以迁移到你想要的模块系统。

    ```javascript
    // bad
    const AirbnbStyleGuide = require('./AirbnbStyleGuide');
    module.exports = AirbnbStyleGuide.es6;

    // ok
    import AirbnbStyleGuide from './AirbnbStyleGuide';
    export default AirbnbStyleGuide.es6;

    // best
    import { es6 } from './AirbnbStyleGuide';
    export default es6;
    ```

  - [9.2](#9.2) <a name='9.2'></a> 不要使用通配符导入模块。

    ```javascript
    // bad
    import * as AirbnbStyleGuide from './AirbnbStyleGuide';

    // good
    import AirbnbStyleGuide from './AirbnbStyleGuide';
    ```

  - [9.3](#9.3) <a name='9.3'></a> 不要导入后立即导出模块。

  > 为什么? 虽然写在一行简洁，但分开有一个清晰的进口和出口，让事情保持一致。

    ```javascript
    // bad
    // filename es6.js
    export { es6 as default } from './airbnbStyleGuide';

    // good
    // filename es6.js
    import { es6 } from './AirbnbStyleGuide';
    export default es6;
    ```

**[返回列表](#table-of-contents)**

## <a name="iterators-and-generators">迭代器和生成器</a>

  - [10.1](#10.1) <a name='10.1'></a> 不要使用迭代器，使用 JavaScript 的高阶函数如 `map()` 和 `reduce()` 替代 `for-of`。

  > 为什么? 这能确保不变性，处理纯函数的返回值相对容易且无副作用。

    ```javascript
    const numbers = [1, 2, 3, 4, 5];

    // bad
    let sum = 0;
    for (let num of numbers) {
      sum += num;
    }

    sum === 15;

    // good
    let sum = 0;
    numbers.forEach((num) => sum += num);
    sum === 15;

    // best (use the functional force)
    const sum = numbers.reduce((total, num) => total + num, 0);
    sum === 15;
    ```

  - [10.2](#10.2) <a name='10.2'></a> 目前不要使用生成器。

  > Why? They don't transpile well to ES5.

**[返回列表](#table-of-contents)**


## <a name="variables">变量</a>

  - [11.1](#11.1) <a name='11.1'></a> 总是使用 `const` 声明变量，使用 `var` 可能会导致全局变量，我们要避免污染全局命名空间。

    ```javascript
    // bad
    superPower = new SuperPower();

    // good
    const superPower = new SuperPower();
    ```

  - [11.2](#11.2) <a name='11.2'></a> 每一个变量都使用一个 `const` 声明。

    > 为什么? 这种方式新增一个变量更容易，不用费劲的去交换 `;` 和 `,`， 又或有时遗漏了。

    ```javascript
    // bad
    const items = getItems(),
        goSportsTeam = true,
        dragonball = 'z';

    // bad
    // (compare to above, and try to spot the mistake)
    const items = getItems(),
        goSportsTeam = true;
        dragonball = 'z';

    // good
    const items = getItems();
    const goSportsTeam = true;
    const dragonball = 'z';
    ```

  - [11.3](#11.3) <a name='11.3'></a> 把所有使用 `const` 和 `let` 的变量分组。

  > 为什么? 当变量随后需要赋值，但它又依赖前一个赋值的变量时将很有帮助。

    ```javascript
    // bad
    let i, len, dragonball,
        items = getItems(),
        goSportsTeam = true;

    // bad
    let i;
    const items = getItems();
    let dragonball;
    const goSportsTeam = true;
    let len;

    // good
    const goSportsTeam = true;
    const items = getItems();
    let dragonball;
    let i;
    let length;
    ```

  - [11.4](#11.4) <a name='11.4'></a> 在需要的时候给变量赋值，但注意把变量放在合理的位置。

  > 为什么？ `let` 和 `const` 具有块级作用域而非函数级作用域。

    ```javascript
    // good
    function() {
      test();
      console.log('doing stuff..');

      //..other stuff..

      const name = getName();

      if (name === 'test') {
        return false;
      }

      return name;
    }

    // bad - unnessary function call
    function(hasName) {
      const name = getName();

      if (!hasName) {
        return false;
      }

      this.setFirstName(name);

      return true;
    }

    // good
    function(hasName) {
      if (!hasName) {
        return false;
      }

      const name = getName();
      this.setFirstName(name);

      return true;
    }
    ```

**[返回列表](#table-of-contents)**


## <a name="hoisting">变量提升</a>

  - [12.1](#12.1) <a name='12.1'></a> `const` and `let` 声明的有一个新概念成为 [暂时性死区(TDZ)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/let#Temporal_dead_zone_and_errors_with_let)。这对于理解 [为什么typeof不再安全](http://es-discourse.com/t/why-typeof-is-no-longer-safe/15) 非常重要。

    ```javascript
    function example() {
      console.log(notDefined); // => throws a ReferenceError
    }

    function example() {
      console.log(declaredButNotAssigned); // => undefined
      var declaredButNotAssigned = true;
    }

    function example() {
      let declaredButNotAssigned;
      console.log(declaredButNotAssigned); // => undefined
      declaredButNotAssigned = true;
    }

    // using const and let
    function example() {
      console.log(declaredButNotAssigned); // => throws a ReferenceError
      console.log(typeof declaredButNotAssigned); // => throws a ReferenceError
      const declaredButNotAssigned = true;
    }
    ```

  - [12.2](#12.2) <a name='12.2'></a> 匿名函数表达式的变量名发生变量提升，它不是一个真正的函数（undefined），不能当函数去调用。

    ```javascript
    function example() {
      console.log(anonymous); // => undefined

      anonymous(); // => TypeError anonymous is not a function

      var anonymous = function() {
        console.log('anonymous function expression');
      };
    }
    ```

  - [12.3](#12.3) <a name='12.3'></a> 具名函数表达式的变量名也会发生变量提升，无论是变量名还是具名函数名都不能当成真正的函数去调用。

    ```javascript
    function example() {
      console.log(named); // => undefined

      named(); // => TypeError named is not a function

      superPower(); // => ReferenceError superPower is not defined

      var named = function superPower() {
        console.log('Flying');
      };
    }

    function example() {
      console.log(named); // => undefined

      named(); // => TypeError named is not a function

      var named = function named() {
        console.log('named');
      }
    }
    ```

  - [12.4](#12.4) <a name='12.4'></a> 函数声明会提升变量名和函数自己，作用域内在声明前可以调用。

    ```javascript
    function example() {
      superPower(); // => Flying

      function superPower() {
        console.log('Flying');
      }
    }
    ```

  - 更多[JavaScript作用域和变量提升](http://www.adequatelygood.com/2010/2/JavaScript-Scoping-and-Hoisting) by [Ben Cherry](http://www.adequatelygood.com/).

**[返回列表](#table-of-contents)**



## Learning ES6

  - [Draft ECMA 2015 (ES6) Spec](https://people.mozilla.org/~jorendorff/es6-draft.html)
  - [ExploringJS](http://exploringjs.com/)
  - [ES6 Compatibility Table](https://kangax.github.io/compat-table/es6/)
  - [Comprehensive Overview of ES6 Features](http://es6-features.org/)



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


