# README 
 
## 背景 
 
该项目基于 JavaScript ES6 以及 TypeScript 2.0.x 制定标准，参考 [Google Code Style](https://google.github.io/styleguide/javascriptguide.xml#var) 以及 [TypeScript Coding Guide](https://github.com/Microsoft/TypeScript/wiki/Coding-guidelines)，其中 JSON 格式的确定参考了 [Google JSON Style Guide](https://google.github.io/styleguide/jsoncstyleguide.xml) 、[Facebook Graph API](https://developers.facebook.com/docs/graph-api/reference)

为了便于 JavaScript 的工程也能使用，我们将 TypeScript 的特定部分单独拆分到一个列表，故在大部分列表中的说明也将适用 JavaScript 工程。

Code Style 主要面向平均水平的工程师，旨在规避语法陷阱，提升开发效率，_可能会部分的摒弃语言本身允许的内容。_ 
 
## Why TypeScript 
 
因为从招聘难易程度(可以招 Java 背景)、代码可读性、其他语言的兼容性来说 TypeScript 更接近其余的 OOP 语言，并且具备了最关键的  Type 功能，在编译时期提供一定的 Type 检查，避免低级错误。 
 
## tslint 
 
建议使用 [tslint](https://github.com/DaYeSquad/tslint-sakura-contrib) 来检查该文档中 Code Style 中的问题 
 
## Webstrom Settings 
 


## JSON 
 
### property name 使用驼峰命名法 
 
DO:
```
{
  "thisIsAPropertyName": "ooxx"
}
``` 
 
###  对于值类型是 array 的使用复数给 propery 命名 
 
DO:
```
{
  // 单数
  "author": "lisa",
  // Array 类型，使用复数
  "siblings": [ "bart", "maggie"],
  // "totalItem" doesn't sound right
  "totalItems": 10,
  // But maybe "itemCount" is better
  "itemCount": 10,
}
``` 
 
###  使用 ISO 8601 标准来表示持续时间 
 
使用 [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601#Durations) 来表示持续时间

DO:
```
{
  // three years, six months, four days, twelve hours,
  // thirty minutes, and five seconds
  "duration": "P3Y6M4DT12H30M5S"
}
``` 
 
###  空值的处理 
 
对于返回值为空的，可以考虑去掉这个值，如:

```
{
  "volume": 10,
  "balance": 0,

  // 去掉 "currentlyPlaying"
  // "currentlyPlaying": null
}
``` 
 
###  使用 string 类型表示 enum 
 
使用 string 类型来表示 enum 而不是 int 类型，这将大大增加返回值的可读性

如在 Java 中:
```
public enum Color {
  WHITE,
  BLACK,
  RED,
  YELLOW,
  BLUE
}
```

则 JSON object:
```
{
  "color": "WHITE"
}
``` 
 
###  使用 RFC 3339 或者 Unix Timestamp 来表示时间点 
 
允许使用 [RFC 3339](https://www.ietf.org/rfc/rfc3339.txt) 或者 Unix Timestamp 来表示时间点

DO:
```
{
  "lastUpdate": "2007-11-06T16:34:41.000Z"
}

{
  "lastUpdateAt": 1477549002 
}
```

**请注意，所谓 Unix Timestamp 只有10位的，13位的叫做毫秒** 
 
 
 
 
###  README 
 
大多数情况下，使用如下命名:
`functionNamesLikeThis`, `variableNamesLikeThis`, `ClassNamesLikeThis`, `EnumNamesLikeThis`, `methodNamesLikeThis`, `CONSTANT_VALUES_LIKE_THIS`, `foo.namespaceNamesLikeThis.bar` 以及 `filenameslikethis.js`,  `filenameslikethis.ts`

私有方法和私有变量使用后下划线来命名，例如`uid_`或者`getSomething_()`

protected 的方法和变量使用和 public 方法变量一样的命名，不使用后下划线，例如`displayName`

**尽可能使用完整的单词而不是缩写来命名** 
 
#### 使用双引号或者 Template String来表示字符串 
 
相对于双引号，推荐使用单引号或者 Template String 语法来表示字符串

tslint
```
"quotemark:" [true, "double", "avoid-escape"]
``` 
 
- 函数变量超过 100 个字符时候需要进行换行 
 
需要在函数字符超过100个/行时进行换行

DO:
```
// Four-space, wrap at 80.  Works with very long function names, survives
// renaming without reindenting, low on space.
goog.foo.bar.doThingThatIsVeryDifficultToExplain = function(
    veryDescriptiveArgumentNumberOne, veryDescriptiveArgumentTwo,
    tableModelEventHandlerProxy, artichokeDescriptorAdapterIterator) {
  // ...
};

// Four-space, one argument per line.  Works with long function names,
// survives renaming, and emphasizes each argument.
goog.foo.bar.doThingThatIsVeryDifficultToExplain = function(
    veryDescriptiveArgumentNumberOne,
    veryDescriptiveArgumentTwo,
    tableModelEventHandlerProxy,
    artichokeDescriptorAdapterIterator) {
  // ...
};

// Parenthesis-aligned indentation, wrap at 80.  Visually groups arguments,
// low on space.
function foo(veryDescriptiveArgumentNumberOne, veryDescriptiveArgumentTwo,
             tableModelEventHandlerProxy, artichokeDescriptorAdapterIterator) {
  // ...
}

// Parenthesis-aligned, one argument per line.  Emphasizes each
// individual argument.
function bar(veryDescriptiveArgumentNumberOne,
             veryDescriptiveArgumentTwo,
             tableModelEventHandlerProxy,
             artichokeDescriptorAdapterIterator) {
  // ...
}
``` 
 
#### 使用空行来组织代码的逻辑 
 
使用空行来视觉分割逻辑

DO:
```
doSomethingTo(x);
doSomethingElseTo(x);
andThen(x);

nowDoSomethingWith(y);

andNowWith(z);
``` 
 
#### 使用 opt_ 前缀表明函数内的某参数为可选参数 
 
如果函数中有变量为可选参数，使用 opt_ 开头

DO:
```
function strangeButTrue(nonNull, mayBeNull, opt_nonNull, opt_mayBeNull) {
  // ...
};
``` 
 
### 注释 
 
- 使用 @license / @preserve 来标记让一些重要的信息(如法律许可或版权信息)原样保留, 同样, 文本中的换行也会被保留 
 
 
 
- 使用 @expose 来声明一个不可修改，消除和优化的属性 
 
 
 
- 使用 @see 来给出引用链接, 用于进一步查看函数 / 方法的相关细节 
 
例如 :

```
/**
 * Adds a single item, recklessly.
 * @see #addSafely
 * @see goog.Collect
 * @see goog.RecklessAdder#add
 ...
``` 
 
- 使用 @author 来表示该文件的作者 
 
描述:
代码的作者，通常只用在 `@fileoverview` 的注释内

样式:
@author username@xx.com
例如:

```
/**
 * @fileoverview Utilities for handling textareas.
 * @author kuth@google.com (Uthur Pendragon)
 */
``` 
 
- 使用 @dict 来指定只能用括号形式来获取属性的对象 
 
例如：

```
/**
 * @constructor
 * @dict
 */
function Foo(x) {
  this['x'] = x;
}
var obj = new Foo(123);
var num = obj.x;  // warning

(/** @dict */ { x: 1 }).x = 123;  // warning
``` 
 
-  使用 @const 来声明变量为只读，或声明方法不可重载和不可重写 
 
例如：

```
/** @const */ var MY_BEER = 'stout';

/**
 * My namespace's favorite kind of beer.
 * @const
 * @type {string}
 */
mynamespace.MY_BEER = 'stout';

/** @const */ MyClass.MY_BEER = 'stout';
``` 
 
-  使用 @define 来声明一个在编译时被重载的常量 
 
例如：

```
/** @define {boolean} */
var TR_FLAGS_ENABLE_DEBUG = true;

/**
 * @define {boolean} Whether we know at compile-time that
 *   the browser is IE.
 */
goog.userAgent.ASSUME_IE = false;
```

在上面例子中, BUILD 文件中指定了 --define='goog.userAgent.ASSUME_IE=true' 

这个编译之后, 常量 goog.userAgent.ASSUME_IE 将被全部直接替换为 true. 
 
- 使用 @supported 在 @fileoverview 中来指定兼容的浏览器 
 
 
 
-  使用 @enum 来声明枚举对象 
 
例如：

```
/**
 * Enum for tri-state values.
 * @enum {number}
 */
project.TriState = {
  TRUE: 1,
  FALSE: -1,
  MAYBE: 0
};
``` 
 
-  使用 @protect 来指明受保护的方法或属性 
 
例如:

```
/**
 * Sets the component's root element to the given element.
 * @param {Element} element Root element for the component.
 * @protected
 */
goog.ui.Component.prototype.setElementInternal = function(element) {
  // ...
};
``` 
 
- 属性注释 
 
例如:
```
/**
 * Maximum number of things per pane.
 * @type {number}
 */
project.MyClass.prototype.someProperty = 4;
``` 
 
- 使用 @typedef 来给一个复杂的类型取一个别名 
 
例如：

```
/** @typedef {(string|number)} */
goog.NumberLike;

/** @param {goog.NumberLike} x A number or a string. */
goog.readNumber = function(x) {
  ...
}
``` 
 
- 使用 @private 来指明私有的方法或属性 
 
/**
 * Handlers that are listening to this logger.
 * @private {!Array.<Function>}
 */
this.handlers_ = []; 
 
- 每个类的定义都要附带一份注释, 描述类的功能和用法 
 
也需要说明构造器参数. 如果该类继承自其它类, 应该使用`@extends` 标记. 如果该类是对接口的实现, 应该使用 `@implements` 标记.

例如:

```
/**
 * Class making something fun and easy.
 * @param {string} arg1 An argument that makes this more interesting.
 * @param {Array.<number>} arg2 List of numbers to be processed.
 * @constructor
 * @extends {goog.Disposable}
 */
project.MyClass = function(arg1, arg2) {
  // ...
};
goog.inherits(project.MyClass, goog.Disposable);
``` 
 
- 使用 @suppress 来忽略警告信息 
 
警告种类以 `|` 或`,`来分隔

例如：

```
/**
 * @suppress {deprecated}
 */
function f() {
  deprecatedVersionOfF();
}
``` 
 
- 使用 @override 来指明子类的方法和属性是故意隐藏了父类的方法和属性. 如果子类的方法和属性没有自己的文档, 就会继承父类的 
 
 
 
- 使用 @export 标记要将名字原样导出的方法 
 
 
 
- 使用 @public 来指明公共的方法或属性 
 
例如：

```
/**
 * Whether to cancel the event in internal capture/bubble processing.
 * @public {boolean}
 * @suppress {visiblity} Referencing this outside this package is strongly
 * discouraged.
 */
 goog.events.Event.prototype.propagationStopped_ = false;
``` 
 
- 使用 @fileoverview 来声明文件相关信息 
 
例如：

```
/**
 * @fileoverview Utilities for doing things that require this very long
 * but not indented comment.
 * @author kuth@google.com (Uthur Pendragon)
 */
``` 
 
- 使用 @nosideeffects 来声明一个没有副作用的函数 
 
用于对函数或构造器声明, 说明调用此函数不会有副作用. 编译器遇到此标记时, 如果调用函数的返回值没有其他地方使用到, 则会将这个函数整个删除

例如：

```
/** @nosideeffects */
function noSideEffectsFn1() {
  // ...
}

/** @nosideeffects */
var noSideEffectsFn2 = function() {
  // ...
};

/** @nosideeffects */
a.prototype.noSideEffectsFn3 = function() {
  // ...
};
``` 
 
- 使用 @template 声明模板 
 
例如：

```
/**
 * @param {function(this:T, ...)} fn
 * @param {T} thisObj
 * @param {...*} var_args
 * @template T
 */
goog.bind = function(fn, thisObj, var_args) {
   ...
};
``` 
 
- 使用 @code 来说明这是一段代码，让它能在生成的文档中正确显示 
 
例如：

```
/**
 * Moves to the next position in the selection.
 * Throws {@code goog.iter.StopIteration} when it
 * passes the end of the range.
 * @return {Node} The node at the next position.
 */
goog.dom.RangeIterator.prototype.next = function() {
  // ...
};
``` 
 
#### README 
 
使用 JSDoc 语法进行注释

所有的文件，类，方法， 属性都需要用对应的标签和类型来进行注释，来说明属性，方法，方法参数，返回值的含义

文件注释中应该写明该文件的基本信息(如, 这段代码的功能摘要, 如何使用, 与哪些东西相关), 来告诉那些不熟悉代码的读者

行内注释使用 `//变量` 的形式 
 
- 使用 @deprecated 来声明一个过时的函数，方法，或属性 
 
常常要指定建议使用的方法

例如：

```
/**
 * Determines whether a node is a field.
 * @return {boolean} True if the contents of
 *   the element are editable, but the element
 *   itself is not.
 * @deprecated Use isField().
 */
BN_EditUtil.isTopEditableField = function(node) {
  // ...
};
``` 
 
- 使用 @return 来给方法，函数的返回值添加说明 
 
例如：

```
/**
 * @return {string} The hex ID of the last item.
 */
goog.Baz.prototype.getLastId = function() {
  // ...
  return id;
};
``` 
 
## 顶层 / 文件注释提供文件的大体内容, 它的作者, 依赖关系和兼容性信息 
 
顶层注释用于告诉不熟悉这段代码的读者这个文件中包含哪些东西

例如:

```JavaScript
// Copyright 2009 Google Inc. All Rights Reserved.

/**
 * @fileoverview Description of file, its uses and information
 * about its dependencies.
 * @author user@google.com (Firstname Lastname)
 */
``` 
 
## 使用 @extends 来声明一个类继承来自的类 
 
例如：

```
/**
 * Immutable empty node list.
 * @constructor
 * @extends goog.ds.BasicNodeList
 */
goog.ds.EmptyNodeList = function() {
  ...
};
``` 
 
## 使用 @noalias 在外部文件中告诉编译器不要为这个变量或函数重命名 
 
 
 
## 使用 @param 来给方法, 函数, 构造器中的参数添加说明 
 
例如 ：

```
/**
 * Queries a Baz for items.
 * @param {number} groupNum Subgroup id to query.
 * @param {string|number|null} term An itemName,
 *     or itemId, or null to search everything.
 */
goog.Baz.prototype.query = function(groupNum, term) {
  // ...
};
``` 
 
## 方法和函数的注释，提供参数的说明 
 
注释使用完整的句子，并用第三人称来书写方法说明

例如:

```
/**
 * Operates on an instance of MyClass and returns something.
 * @param {project.MyClass} obj Instance of MyClass which leads to a long
 *   comment that needs to be wrapped to two lines.
 * @return {boolean} Whether something occurred.
 */
function PR_someMethod(obj) {
  // ...
}
``` 
 
## 使用 @nocompile 在文件上方指定该文件不被编译 
 
 
 
## 使用 @externs 来声明一个外部文件 
 
 
 
## 使用 @struct 在构造方法中来声明那些“ . ”形式获取属性的类 
 
并且，对象创建以后，不允许添加新的属性

例如：

```
/**
 * @constructor
 * @struct
 */
function Foo(x) {
  this.x = x;
}
var obj = new Foo(123);
var num = obj['x'];  // warning
obj.y = "asdf";  // warning

Foo.prototype = /** @struct */ {
  method1: function() {}
};
Foo.prototype.method2 = function() {};  // warning
``` 
 
## 使用 @type  来指明变量，属性，表达式的类型 
 
例如：

```
/**
 * The message hex ID.
 * @type {string}
 */
var hexId = hexId;
``` 
 
## 使用 @implements 来声明类实现的接口 
 
例如：

```
/**
 * A shape.
 * @interface
 */
function Shape() {};
Shape.prototype.draw = function() {};

/**
 * @constructor
 * @implements {Shape}
 */
function Square() {};
Square.prototype.draw = function() {
  ...
};
``` 
 
## 使用 @this 来指明调用这个方法时, 需要在哪个上下文中 
 
当 this 指向的不是原型方法的函数时必须使用这个标记

例如：

```
pinto.chat.RosterWidget.extern('getRosterElement',
/**
 * Returns the roster widget element.
 * @this pinto.chat.RosterWidget
 * @return {Element}
 */
function() {
  return this.getWrappedComponent_().getElement();
});
``` 
 
## 在注释内换行，需要遵守和代码段一样的缩进长度 
 
DO:
```
/**
 * Illustrates line wrapping for long param/return descriptions.
 * @param {string} foo This is a param with a description too long to fit in
 *   one line.
 * @return {number} This returns something that has a description too long to
 *   fit in one line.
 */
project.MyClass.prototype.method = function(foo) {
  return 5;
};
```

DON'T:
```
/**
 * This is NOT the preferred indentation method.
 * @param {string} foo This is a param with a description too long to fit in
 *                     one line.
 * @return {number} This returns something that has a description too long to
 *                  fit in one line.
 */
project.MyClass.prototype.method = function(foo) {
  return 5;
};
```


` @fileoverview` 注释不应该换行，`@desc`不建议换行 
 
## 使用 @constructor 来声明类的构造器 
 
 
 
## 使用 @lends 表示把对象的键看成是其他对象的属性 
 
例如：

```
goog.object.extend(
    Button.prototype,
    /** @lends {Button.prototype} */ {
      isButton: function() { return true; }
    });
``` 
 
 
 
 
# 语法部分 
 
## 使用 const 来声明常量 
 
应当使用 `const` 关键字来声明常量。

DO:
```JavaScript
const BASE_URL = 'http://localhost:3000';
``` 
 
## 使用 let，不要使用 var 
 
`var` 在作用域方面有着麻烦的问题，例如
```JavaScript
var a = 5;
if(true){
    var a = 10;
}
console.log(a); // 由于 a 共用内存地址，故此处为10
```

而 ES6 引入的 `let` 则没有相似的问题，在作用域方面，`let`与`const`都是块级作用域(与你所想一致)。

DO:
```
let a = 5;
if(true){
    let a = 10;
}
console.log(a); // 5
```

DON'T:
```
var a = 5;
if(true){
    var a = 10;
}
console.log(a); // 10
```

tslint: 
```
"no-var-keyword": true
``` 
 
## 不要将基础类型当对象使用 
 
DON'T:
```
let x = new Boolean(false);
if (x) { // x 作为 object 存在
  alert('hi');  // Shows 'hi'.
}
```

但是在对类型进行强制转换的时候 Wrapper 是很有用的。

DO:
```
let x = Boolean(0);
if (x) {
  alert('hi');  // This will never be alerted.
}
typeof Boolean(0) == 'boolean';
typeof new Boolean(0) == 'object';
``` 
 
## 使用 + 或者 template string 来对多行 string 进行换行 
 
DO:
```
let myString = 'A rather long string of English text, an error message ' +
    'actually that just keeps going and going -- an error ' +
    'message to make the Energizer bunny blush (right through ' +
    'those Schwarzenegger shades)! Where was I? Oh yes, ' +
    'you\'ve got an error and all the extraneous whitespace is ' +
    'just gravy.  Have a nice day.';
```

OR

```
let mystring = ` A rather long string of English text, an error message
                actually that just keeps going and going -- an error
                message to make the Energizer bunny blush (right through
                those Schwarzenegger shades)! Where was I? Oh yes,
                you\'ve got an error and all the extraneous whitespace is
                just gravy.  Have a nice day.`;
```

DON'T:
```
let myString = 'A rather long string of English text, an error message \
                actually that just keeps going and going -- an error \
                message to make the Energizer bunny blush (right through \
                those Schwarzenegger shades)! Where was I? Oh yes, \
                you\'ve got an error and all the extraneous whitespace is \
                just gravy.  Have a nice day.';
``` 
 
## 所有的 if else 都必须使用大括号 
 
哪怕判断的实现代码只有一行，都应该使用 {}

DO:
```
if (foo) {
  // do...
}
```

DON'T:
```
if (foo) // don't
``` 
 
## this 
 
尽量只在类的构造函数、方法和 closure 中使用 `this`。

`this`是一个复杂的语法，大多数时候它指向了全局的对象，在某些方法中它指向了实例，有时候...

所以限制 `this` 的使用看起来就像是一个必须的事情了，我们建议只在类中使用 `this`。 
 
## 必须使用分号作为结尾 
 
DO:
```JavaScript
let foo = function() {
  return true;
};  // semicolon here.

function foo() {
  return true;
}  // no semicolon here.
```

tslint:
```
"semicolon": [
      true,
      "always",
      "ignore-bound-class-methods"
    ]
``` 
 
## 不要在函数块内声明函数 
 
DO:
```
if (x) {
  var foo = function() {};
}
```

DON'T:
```
if (x) {
  function foo() {}
}
``` 
 
## 仅在遍历 keys 的时候使用 for-in 循环 
 
`for-in` 循环在遍历 `array` 类型的时候往往被错误的使用，`for-in` 是用来遍历 keys 的，如果在 `array` 中使用，应当考虑使用最基本的循环方法或者 `for-of` 循环。

以下两种方式是对等的
```
for (let key in arr){
    console.log(arr[key]);
}

for (let value of arr){
    console.log(value);
}

for (let i = 0; i < 1; arr.length){
    console.log(arr[i]);
}
```

DO:
```
for (let value of arr){
    console.log(value);
}

for (let i = 0; i < 1; arr.length){
    console.log(arr[i]);
}
``` 
 
# TypeScript 部分 
 
- 每个文件代表一个逻辑组件，如 checker, emitter 等 
 
 
 
- 使用 Array<T> 表示可变数组，使用 T[] 表示不可变数组 
 
 
 
- 使用 undefined 而不是 null 
 
 
 
- 不要使用 "I" 来作为 interface 的前缀 
 
 
 
- 共享的类型声明应放置在 'types.ts' 中 
 
 
 
- 对于非公有变量推荐使用 private 或者 protected 修饰符来声明 
 
 
 
# 其他 
 
## 所有用户可见的字符串都必须做国际化 
 
所有用户可见的字符串都必须存储在国际化文件中

**Node:**
在佳格中，我们在 Node 中使用 [i18n-node](https://github.com/mashpie/i18n-node) 作为国际化的库

**React:**
在佳格中，我们在 React 中使用 [React-intl](https://github.com/yahoo/react-intl) 作为国际化的库，需要注意的是该库(2.0.29)在 TypeScript 中的 npm 包中有一处[错误](https://github.com/DefinitelyTyped/DefinitelyTyped/blob/types-2.0/react-intl/react-intl-tests.tsx)，需要自己手动增加一个声明用于 props 的继承:

```JavaScript
// Copyright 2016 Frank Lin (lin.xiaoe.f@gmail.com). All rights reserved.
// Use of this source code is governed a license that can be found in the LICENSE file.

import { InjectedIntlProps } from "react-intl";

/**
 * https://github.com/DefinitelyTyped/DefinitelyTyped/tree/types-2.0/react-intl 中所给出的 react-intl-tests.tsx 的例子
 * 是错误的，应该使用 this.props.intl.formatMessage 而不是 this.props.formatMessage，该文件用于修正该错误。
 */
export interface ReactIntlProps {
  intl?: InjectedIntlProps;
}
```

示例见 https://github.com/DefinitelyTyped/DefinitelyTyped/blob/types-2.0/react-intl/react-intl-tests.tsx，其中 this.props.formatMessage 应当换成 this.props.intl.formatMessage 
 
## 推荐使用 arrow function 语法相对于匿名函数 
 
 
 
## 路由的 URL 使用全部小写的写法 
 
由于浏览器不区分大小写，所以 URL 使用全小写的方式

DO:
`/send_initial_password`

DON'T:
`/sendInitialPassword` 
 
# 命名 
 
## 使用两个空格缩进并且将 tab 设置为空格 
