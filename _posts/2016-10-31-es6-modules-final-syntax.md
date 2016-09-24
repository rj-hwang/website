---
layout: blog
title: 【译】ECMAScript 6 模块：最终语法
---

# {{page.title}}

---------------

本博客的最新更新版本请移步原作在线书籍 “[Exploring ES6](http://exploringjs.com/es6/)” 的 “[Modules](http://exploringjs.com/es6/ch_modules.html)” 章节。

---------------

[TC39](http://www.ecma-international.org/memento/TC39.htm) 技术委员会在 2014 年 7 月底的一个[会议](https://github.com/rwaldron/tc39-notes/tree/master/es6/2014-07)中，敲定了 ECMAScript 6 (ES6) 模块语法的细节。本博客文章对 ES6 模块系统来一个全面的综述。

## 1. 当前的 JavaScript 模块系统
JavaScript 没有内置的模块支持，不过社区却创建了两个令人印象深刻的变通处理，其中两个最重要的标准（不幸的是这两个标准互不兼容）是：

- CommonJS Modules：这个标准的主要实现是在 Node.js（Node.js 模块在 CommonJS 之上又扩展了一些额外的特征），特点：
	- 简洁的语法
	- 为同步加载而设计
	- 主要用途：服务端

- Asynchronous Module Definition (AMD)：这个标准最流行的实现是 [RequireJS]，特点：
	- 稍微复杂的语法，允许 AMD 不使用 eval()（或在编译时）。
	- 为异步加载而设计
	- 主要用途：浏览器端

上面只是非常简单的介绍，如果要深入了解，可以参考 Addy Osmani 的 "[Writing Modular JavaScript With AMD, CommonJS & ES Harmony]"

## 2. ECMAScript 6（ES6） 模块
ECMAScript 6 模块的目的是创建兼容 CommonJS 和 AMD 两者的格式：

- 类似于 CommonJS，有简洁的语法，通过 exports 导出和支持循环依赖。
- 类似于 AMD，直接支持异步加载和通过配置加载

基于 ES6 构建的模块将超越 CommonJS 和 AMD（后面会详细解析）：

- 语法比 CommonJS 还简单
- 可以静态分析模块的结构（静态检测、优化等）
- 对循环依赖的支持比 CommonJS 还好

ES6 模块标准分为两部分：

- 声明式的语法（为了导入和导出）
- 可编程的加载 API：可配置模块的加载方式和按条件加载模块

## 3. ES6 模块语法概述
有两种方法导出：按名称导出（每个模块导出多个）和默认导出（每个模块仅导出一个）。  
注：英文原义为 named exports 和 default exports。

### 3.1 按名称导出（每个模块导出多个东东）- Named exports
模块通过指定关键字来导出多个东东，导出的东东通过名称进行区分，这种导出方式称为按名称导出（Named exports）。

```js
//------ lib.js ------
export const sqrt = Math.sqrt;
export function square(x) {
  return x * x;
}
export function diag(x, y) {
  return sqrt(square(x) + square(y));
}

//------ main.js ------
import { square, diag } from 'lib';
console.log(square(11)); // 121
console.log(diag(4, 3)); // 5
```

还有其它的方式来指定导出的名称（后面会解析），不过上述这个方式相当便捷：按常规方式写下你的代码，然后简单的给它打个标签以指定的关键字导出。

如果你喜欢，你可以导入整个模块然后通过名称引用该模块导出的东东：

```js
//------ main.js ------
import * as lib from 'lib';
console.log(lib.square(11)); // 121
console.log(lib.diag(4, 3)); // 5
```

**相同代码的 CommonJS 语法：** 有一段时间，试过几个聪明的策略来减少 Node.js 模块的冗余导出。现在更喜欢下面的简单但稍微详细的风格，这种风格让人联想起 [revealing module pattern] （模块模式）：

```js
//------ lib.js ------
var sqrt = Math.sqrt;
function square(x) {
  return x * x;
}
function diag(x, y) {
  return sqrt(square(x) + square(y));
}
module.exports = {
  sqrt: sqrt,
  square: square,
  diag: diag,
};

//------ main.js ------
var square = require('lib').square;
var diag = require('lib').diag;
console.log(square(11)); // 121
console.log(diag(4, 3)); // 5
```

### 3.2 默认导出（每个模块仅导出一个东东）- Default exports
在 Node.js 社区，模块仅导出一个值的情形相当普遍。在前端开发中，如果经常使用 constructors/classes 的单一组件模式，这种情形也是很常用的。ES6 模块选择默认导出这种最重要的导出值的方式。使用默认导出方式的模块在导入时特别简单。

下面的这个 ES6 模块是一个单纯的函数：

```js
//------ myFunc.js ------
export default function () { ... };

//------ main1.js ------
import myFunc from 'myFunc';
myFunc();
```

如果默认导出的是一个类，则其代码如下：

```js
//------ MyClass.js ------
export default class { ... };

//------ main2.js ------
import MyClass from 'MyClass';
let inst = new MyClass();
```

注：默认导出的操作对象是一个[表达式]，它通常没有名称，而是通过模块的名称来标识。

### 3.3 在模块中同时使用按名称导出和默认导出
下面的模式在JavaScript中非常普遍：通过函数的属性提供附加服务的函数库。如 jQuery 和 Underscore.js。如下是 Underscore 作为 CommonJS 模块的代码片段：

```js
//------ underscore.js ------
var _ = function (obj) {
  ...
};
var each = _.each = _.forEach =
  function (obj, iterator, context) {
    ...
  };
module.exports = _;

//------ main.js ------
var _ = require('underscore');
var each = _.each;
...
```

如果使用 ES6，函数 `_` 使用默认导出，`each` 和 `forEach` 使用按名称导出。这个就是在模块中同时使用按名称导出和默认导出的真实案例。作为一个例子，上面的 CommonJS 模块使用 ES6 模块重写后的代码如下：

```js
//------ underscore.js ------
export default function (obj) {
  ...
};
export function each(obj, iterator, context) {
  ...
}
export { each as forEach };

//------ main.js ------
import _, { each } from 'underscore';
...
```

上面的 CommonJS 版和 ES6 版的代码大致相似。后者的代码是扁平风格，而前者是嵌套风格。哪种更好就看个人喜好了，但后者扁平风格的好处是能进行静态分析（后面再解析为什么）。前者的 CommonJS 风格似乎是出于要将对象视作命名空间来使用的需要，通常这种情形是完全可以通过 ES6 模块的按名称导出来实现。

**默认导出只是按名称导出的一个特例**

其实默认导出只是一个使用 'default' 作为名称的按名称导出方式。也就是说下面两行代码是等同的：

```js
import { default as foo } from 'lib';
import foo from 'lib';
```
类似的，下面两个模块具有相同的默认导出：

```js
//------ module1.js ------
export default 123;

//------ module2.js ------
const D = 123;
export { D as default };

```

**为什么需要按名称导出呢？**

你可能想知道 － 如果我们可以简单的默认导出一个对象（像 CommonJS），为什么我们需要按名称导出呢？答案就是你无法通过对象来实施一个静态结构以及失去所有的相关优势（下章再说明）。

## 4. 设计目标
下面主要的几点将有助于您理解 ECMAScript 6 模块的设计目标：

- 默认导出备受欢迎
- 静态模块结构
- 同时支持同步和异步加载
- 支持模块间的循环依赖

以下将逐个进行解析。

### 4.1 默认导出备受欢迎
默认导出的语法看起来感觉有点陌生，不过基于要让默认导出尽可能的简便这一重要设计目标，就能明白为何这样做了。引用一下 [David Herman] 的话:

> ECMAScript 6 喜好模块的单一默认导出方式，同时也提供了甜蜜的语法来将其导入。导入按名称导出的东东就稍微没有那么简洁了。

### 4.2 静态模块结构
在当前的 JavaScript 模块系统中，需要先执行模块代码才能找出要导入和导出的东东。这是 ECMAScript 6 与这些模块系统断裂的主要原因：ES6 的模块系统语言，语法上就是一个稳健的静态模块结构。让我先解析一下这意味什么以及这样能带来什么好处。

如果模块的结构是静态的，那么在编译时（静态的）就可以决定要导入和导出什么 － 只需查看源代码，无需解析代码。下面的两个例子表明 CommonJS 模块为什么做不到这点。第一个例子，必须执行代码才能知晓导入了什么：

```js
var mylib;
if (Math.random()) {
  mylib = require('foo');
} else {
  mylib = require('bar');
}
```

第二个例子，也必须执行代码才能知晓导入了什么：

```js
if (Math.random()) {
  exports.baz = ...;
}
```

ECMAScript 6 给与了更少的灵活性，它强制代码结构必须是静态的。结果是优点多多 [[2]]，下面会继续说明。

**优点 1：查找更快**

在 CommonJS 中获取一个模块依赖，将得到一个对象：

```
var lib = require('lib');
lib.someFunc(); // property lookup
```

然后通过 `lib.someFunc` 这个名称查找并获取这个方法，这种动态查找方式是缓慢的。  
对比来看看，如果你导入一个 ES6 模块的库函数，通过静态的方式就可以知晓它的内容，从而可以优化获取的方法：

```js
import * as lib from 'lib';
lib.someFunc(); // statically resolved
```

**优点 2：变量检测**

使用静态的模块结构，随时可以静态的分析知晓模块中哪些变量在哪些范围内是可见的：

- 全局变量：全局变量将渐渐只来自语言自身提供的，其它的变量都将来自模块（包括函数库和浏览器提供的功能）。也就是说您可以通过静态检测，知晓所有的全局变量。
- 导入模块：也可以通过静态检测获知。
- 模块的内部变量：通过静态监测，也可以得出。

这对检测变量的标识符是否拼写正确提供极大的帮助。这种类型的检测在 JSLint 和 JSHint 中十分普遍。而在 ECMAScript 6 中，大多数是通过 JavaScript 引擎自身进行检测的。

另外，任何通过按名称导出的属性方法（如 lib.foo）的访问，也可静态检测到。

**优点 3：为宏作好准备**

宏仍在 JavaScript 未来路线图的规划中。如果 JavaScript 引擎支持宏，您就可以通过函数库添加新的语法。[Sweet.js] 就是一个 JavaScript 宏系统的实验性项目。如下是 Sweet.js 网站的一个例子：为类添加一个宏。

```js
// Define the macro
macro class {
  rule {
    $className {
        constructor $cparams $cbody
        $($mname $mparams $mbody) ...
    }
  } => {
    function $className $cparams $cbody
    $($className.prototype.$mname
      = function $mname $mparams $mbody; ) ...
  }
}

// Use the macro
class Person {
  constructor(name) {
    this.name = name;
  }
  say(msg) {
    console.log(this.name + " says: " + msg);
  }
}
var bob = new Person("Bob");
bob.say("Macros are sweet!");
```

JavaScript 引擎在编译之前就执行宏的预处理：如果一个序列令牌被宏模式解析匹配到，它将被宏的 body 替换。如果希望在预处理阶段通过静态检测发现宏的定义，并通过模块导入宏，代码必须是静态结构的。

**优点 4：为类型作好准备**

静态类型检测须像宏一样添加强制性约束：只有类型的定义代码是静态结构的，才能进行静态类型检测。再者，只有类型声明是静态结构的，类型才能从模块中导入。

类型是吸引人的，因为在编写性能关键型的代码时，可以启用静态类型快速方言。如 [Low-Level JavaScript (LLJS)]，目前编译为 [asm.js]。

**优点 5：支持其它语言**

如果要支持编译带宏和静态类型的 JavaScript，就如前面两章提到的原因，JavaScript 模块就应该有一个静态结构。

### 4.3 同时支持同步和异步加载
无论引擎是同步（如服务端）还是异步（如在浏览器端）加载模块，ECMAScript 6 模块都必须能独立运转。其语法更适合于同步加载，通过其静态结构启用异步加载：因可以静态分析决定所有导入，在解析模块的代码前可先加载（这方式让人想起 AMD 模块）。

### 4.4 支持模块间的循环依赖
如果模块 A（直接或间接） 导入 模块 B 而 B 又导入 A 则这两个模块之间就是[[循环依赖]]。如果可能的话应该避免循环依赖，这会导致 A 和 B 紧密耦合 － 它们就只能一起使用和发展。

**为什么支持循环依赖呢？**

循环依赖并不一定有害。尤其是对象，甚至有时希望有这种依赖：例如，在一些树形结构中（如 DOM 文档），父节点引用子节点，子节点又反过来引用父节点。通过小心的设计通常都可以避免循环依赖。然而在一个大型的系统中，循环依赖经常发生，特别是在重构时。因此如果一个模块系统支持循环依赖是非常有用的，这样在系统重构时就不会被阻断。

Node.js 的文档承认了循环依赖的重要性[[3]]，Rob Sayre 提供了额外的[证据]：

> 数据点：我曾经为 Firefox 实现了一个类似 \[ECMAScript 6 模块\] 的系统，发布 3 周后我就收到了要求支持循环依赖的[请求]。  
	这个由 Alex Fritze 发明并且我参与了的系统不是很完美，而且语法也不怎么好。但一样持续使用了 7 年，所以它也一定是做了一些正确的事情。

让我们瞧瞧 CommonJS 和 ECMAScript 6 是怎样处理循环依赖的。

**CommonJS 中的循环依赖**

在 CommonJS 中，如果模块 B require 一个当前已经解析执行的模块 A，得到的是 A 当前状态的导出对象（下面例子中标号为 1 的地方）。这样 B 就可以引用 A 所导出对象中的属性方法（标号 2）。这个属性方法要在 B 解析执行完成之后才能正确引用到，基于这一点 B 模块的导出才能正常工作。

```js
//------ a.js ------
var b = require('b');
exports.foo = function () { ... };

//------ b.js ------
var a = require('a'); // (1)
// Can’t use a.foo in module body,
// but it will be filled in later
exports.bar = function () {
  a.foo(); // OK (2)
};

//------ main.js ------
var a = require('a');
```

作为一般规则，记住在循环依赖中，你不能在模块的主体代码处访问导入模块所导出的对象。这一固有的现象在 ECMAScript 6 模块中也是一样。

CommonJS 处理方式的局限性：

- Node.js 风格的单一值导出无法正常工作。在 Node.js 中可以导出单一的值而不是导出一个对象，如：  
	`module.exports = function () { ... }`  
	如果在模块 A 中这样写，在模块 B 中就不能使用到这个导出的函数，因为 B 的变量 a 指向的是模块 A 的原始导出对象。
- 无法直接使用按名称导出的属性方法。即模块 B 不能像如下那样导入 a.foo：  
	`var foo = require('a').foo;`  
	foo 的值将是 undefined。只可通过导出的对象 a 去引用 foo，没有任何其它的方法。

CommonJS 有一个独特的特点：你可以在导入前导出。这样的导出可以保证在模块的主体代码中能访问到。即如果 A 这样写代码，就可以在 B 的主体代码中访问到。不过这种情况极少使用到。

**ECMAScript 6 中的循环依赖**

为了消除上述的两个限制，ECMAScript 6 模块导出的是绑定（bindings）而不是值（values）。即连接到模块主体中声明的变量是活的。下面的代码演示了这点：

```js
//------ lib.js ------
export let counter = 0;
export function inc() {
  counter++;
}

//------ main.js ------
import { inc, counter } from 'lib';
console.log(counter); // 0
inc();
console.log(counter); // 1
```

因此，对循环依赖，不管您是直接访问指定名称的导出，还是通过整个模块来访问：在这两种情况下总有一个间接的调用来保证代码总是能工作。

## 5. 导入和导出的各种方式

### 5.1 导入

ECMAScript 6 提供如下几种导入方式 [[4]][Imports]：

```js
// 默认导出和按名称导出
import theDefault, { named1, named2 } from 'src/mylib';
import theDefault from 'src/mylib';
import { named1, named2 } from 'src/mylib';

// 重命名：将 named1 导入为 myNamed1
import { named1 as myNamed1, named2 } from 'src/mylib';

// 将模块导入为一个对象
// (每个导出项作为该对象的一个属性)
import * as mylib from 'src/mylib';

// 仅加载模块不导入任何东东
import 'src/mylib';
```

### 5.2 导出

可以通过两种方式导出当前模块中的项 [[5]][Exports]。一种是通过 export 关键字声明导出项：

```js
export var myVar1 = ...;
export let myVar2 = ...;
export const MY_CONST = ...;

export function myFunc() {
  ...
}
export function* myGeneratorFunc() {
  ...
}
export class MyClass {
  ...
}
```

对于默认导出，其目标对象是一个表达式（包括函数表达式和类表达式），如：

```js
export default 123;
export default function (x) {
  return x
};
export default x => x;
export default class {
  constructor(x, y) {
    this.x = x;
    this.y = y;
  }
};
```

另一种方式是在模块的底部一次过列出所有要导出的项（类似于模块模式所展现的风格）：

```js
const MY_CONST = ...;
function myFunc() {
  ...
}

export { MY_CONST, myFunc };
```

也可以如下所示导出为不同的名称：

```js
export { MY_CONST as THE_CONST, myFunc as theFunc };
```

要注意的是，不能使用保留字（如 default 和 new）作为变量名称，但可以用作导出的名称（在 ECMAScript 5 中也可以作为属性名使用）。如果要导入使用了保留字作为导出名称的项，则导入时需要重命名它们为合适的变量名。

### 5.3 重新导出

重新导出是指将其它模块的导出添加到当前模块的导出中。如下为添加其它模块的所有导出项：

```js
export * from 'src/other_module';
```

或者如下有选择的导出（可选择同时重命名）：

```js
export { foo, bar } from 'src/other_module';

// 导出 other_module 模块的 foo 为 myFoo
export { foo as myFoo, bar } from 'src/other_module';
```

## 6. eval() 和模块
eval() 不支持模块语法。eval 是按脚本语法规则对其参数进行解析，而脚本是不支持模块语法的（后面会解析原因）。如果你想执行模块代码，就必须使用模块加载器 API（后面再说明）。

## 7. ECMAScript 6 模块加载器 API

除了声明性的模块语法，还有一个[可编程 API 接口]，它允许：

- 以编程的方式处理模块和脚本
- 配置模块加载方式

加载器通过模块标识符 (import ... from 语句最后面的字符串 ID) 来加载模块。各个平台使用全局系统变量 System (系统加载器) 来实现模块加载。

### 7.1 模块导入和脚本加载

通过 [ES6 Promise] API 以编程的方式导入模块：

```js
System.import('some_module')
.then(some_module => {
  // Use some_module
})
.catch(error => {
  ...
});
```

System.import() 允许你：

- 在 &lt;script type="module"&gt; 或 &lt;module&gt; 标签内使用模块
- 按条件加载模块

System.import() 只能导入一个模块，不过可以使用 Promise.all() 导入多个模块：

```js
Promise.all(
  ['module1', 'module2', 'module3']
  .map(x => System.import(x)))
.then(([module1, module2, module3]) => {
  // Use module1, module2, module3
});
```

其它方法：

- [System.module(source, options?)](https://people.mozilla.org/~jorendorff/es6-draft.html#sec-reflect.loader.prototype.module) 解析执行 JaveScript 源代码为模块（通过 promise 异步返回解析执行的结果）。
- [System.set(name, module)](https://people.mozilla.org/~jorendorff/es6-draft.html#sec-reflect.loader.prototype.set) 注册模块（如将 System.module() 解析执行的结果注册为一个模块）。
- [System.define(name, source, options?)](https://people.mozilla.org/~jorendorff/es6-draft.html#sec-reflect.loader.prototype.define) 解析执行模块代码后立即注册。

### 7.2 模块加载方式的配置

模块加载器 API 有好几个变种的配置方式，它们仍然处在发展阶段。第一个浏览器端的系统加载器当前已实现和测试通过。目标是找出更好的可配置的模块加载方式。

加载器 API 允许多种自定义的加载过程，如：

1. 导入时对模块进行静态代码分析 (如通过 JSLint 或者 JSHint).
2. 导入时自动转换模块 (如转换 CoffeeScript 或者 TypeScript 代码).
3. 使用传统的模块 (AMD, Node.js)。

Node.js 和 CommonJS 对模块加载过程的可配置性是受限制的。

## 8. 补充信息

如下内容回答了 ECMAScript 6 模块两个重要的问题：现在怎么使用？如何嵌入到 HTML 中？

- **[“Using ECMAScript 6 today”](http://www.2ality.com/2014/08/es6-today.html)** 这篇文章对 ECMAScript 6 进行了概述并解析了如何编译为 ECMAScript 5。如果你感兴趣的是后者，可以阅读 [Sect 2](http://www.2ality.com/2014/08/es6-today.html#using_ecmascript_6_today)。一个有趣的小型解决方案是 [ES6 Module Transpiler](https://github.com/esnext/es6-module-transpiler)，它仅在 ES5 中添加 ES6 模块语法，并编译为 AMD 或者 CommonJS。
- **在 HTML 中嵌入 ES6 模块**: &lt;script&gt; 标签内的代码不支持模块语法， 因为其同步的特性与模块的异步特征不兼容。需要使用 &lt;module&gt; 标签替换。 [“ECMAScript 6 modules in future browsers”](http://www.2ality.com/2013/11/es6-modules-browsers.html) 这篇博客解析了 &lt;module&gt; 是如何工作的。它有几个超越 &lt;script&gt; 的显著优点，不过也可使用 &lt;script type="module"&gt;。
- **CommonJS vs ES6**: [“JavaScript Modules”](http://jsmodules.io) (by [Yehuda Katz](https://github.com/wycats/jsmodules)) 是 ECMAScript 6 模块的一个快速简介。特别有趣的是[第二页](http://jsmodules.io/cjs.html)，将 CommonJS 模块与其 ECMAScript 6 版本的模块代码进行并排显示对比。

## 9. ECMAScript 6 模块的好处

咋一看，将模块构建为 ECMAScript 6 可能看起来像是一个无聊的特征 － 毕竟我们已经有好几个良好的模块系统。但是 ECMAScript 6 模块拥有无法通过添加一个库就能拥有的特征，如非常紧凑的语法和静态模块结构（这有助于优化、静态检测甚至更多）。ECMAScript 6 模块还将 － 希望 － 终结目前占主导地位的 CommonJS 和 AMD 模块标准之间的分裂。

拥有原生的模块标准意味着：

- 不再需要 UMD ([Universal Module Definition](https://github.com/umdjs/umd)): UMD 模式适用于多种模块系统（如 CommonJS 和 AMD）。一旦 ES6 成为唯一的模块标准，UMD 就会被淘汰。
- 新的浏览器 API 将替代全局变量或者 navigator 中的属性而变得模块化。
- 不再需要对象命名空间: 诸如 Math 和 JSON 对象在 ECMASript 5 中是作为函数的名称空间提供服务。日后这些功能函数将通过模块的方式提供。

**致谢：**多谢 Domenic Denicola [确认](http://esdiscuss.org/topic/es6-module-syntax-done#content-2)模块的最终语法。多谢 Guy Bedford、John K. Paul、Mathias Bynens、Michael Ficarra 对此 blog 的更正。

## 10. 参考
1. 原文链接（英文）：[ECMAScript 6 modules: the final syntax] - 2014-09-07
1. [A JavaScript glossary: ECMAScript, TC39, etc.]
2. "[Static module resolution]" by David Herman
3. "[Modules: Cycles]" in the Node.js API documentation
4. "[Imports]" (ECMAScript 6 specification)
5. "[Exports]" (ECMAScript 6 specification)


[ECMAScript 6 modules: the final syntax]: http://www.2ality.com/2014/09/es6-modules-final.html
[RequireJS]: http://requirejs.org
[Writing Modular JavaScript With AMD, CommonJS & ES Harmony]: http://addyosmani.com/writing-modular-js
[revealing module pattern]: http://christianheilmann.com/2007/08/22/again-with-the-module-pattern-reveal-something-to-the-world/
[表达式]: http://speakingjs.com/es5/ch07.html#expr_vs_stmt
[David Herman]: http://esdiscuss.org/topic/moduleimport#content-0
[2]: http://www.2ality.com/2014/09/es6-modules-final.html#[2]
[Sweet.js]: http://sweetjs.org
[Low-Level JavaScript (LLJS)]: http://lljs.org
[asm.js]: http://www.2ality.com/2013/02/asm-js.html
[循环依赖]: http://en.wikipedia.org/wiki/Circular_dependency
[3]: http://www.2ality.com/2014/09/es6-modules-final.html#[3]
[证据]: https://mail.mozilla.org/pipermail/es-discuss/2014-July/038250.html
[请求]: https://bugzilla.mozilla.org/show_bug.cgi?id=384168#c7
[it's still getting used]: https://developer.mozilla.org/en-US/docs/Mozilla/JavaScript_code_modules/Using
[可编程 API 接口]: https://people.mozilla.org/~jorendorff/es6-draft.html#sec-loader-objects

[A JavaScript glossary: ECMAScript, TC39, etc.]: http://www.2ality.com/2011/06/ecmascript.html
[Static module resolution]: http://calculist.org/blog/2012/06/29/static-module-resolution
[Modules: Cycles]: http://nodejs.org/api/modules.html#modules_cycles
[Imports]: https://people.mozilla.org/~jorendorff/es6-draft.html#sec-imports
[Exports]: https://people.mozilla.org/~jorendorff/es6-draft.html#sec-exports
[ES6 Promise]: http://www.html5rocks.com/en/tutorials/es6/promises