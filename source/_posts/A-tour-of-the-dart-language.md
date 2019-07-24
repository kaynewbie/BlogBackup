---
title: Dart 入门 (译)
tags: 
- dart
- flutter
date: 2019-07-24 23:33:48
---

本文列出了 Dart 语言的每个主要功能的用法，从变量和运算符到类库。本文适用于有其他编程语言经验的开发者。
想学习更多 Dart 核心库的，请查看此[文档](https://dart.dev/guides/libraries/library-tour)。想学习更多语言细节的，请查看此[文档](https://dart.dev/guides/language/spec)。
<!-- more -->

目录
- [1. 一段基础的 Dart 程序](#1-%e4%b8%80%e6%ae%b5%e5%9f%ba%e7%a1%80%e7%9a%84-dart-%e7%a8%8b%e5%ba%8f)
- [2. 重要概念](#2-%e9%87%8d%e8%a6%81%e6%a6%82%e5%bf%b5)
- [3. 关键字](#3-%e5%85%b3%e9%94%ae%e5%ad%97)
- [4. 变量](#4-%e5%8f%98%e9%87%8f)
  - [4.1 默认值](#41-%e9%bb%98%e8%ae%a4%e5%80%bc)
  - [4.2 Final 和 const 关键字](#42-final-%e5%92%8c-const-%e5%85%b3%e9%94%ae%e5%ad%97)
- [5. 自带类型](#5-%e8%87%aa%e5%b8%a6%e7%b1%bb%e5%9e%8b)
  - [5.1 数值](#51-%e6%95%b0%e5%80%bc)
  - [5.2 字符串](#52-%e5%ad%97%e7%ac%a6%e4%b8%b2)
  - [5.3 布尔](#53-%e5%b8%83%e5%b0%94)
  - [5.4 数组](#54-%e6%95%b0%e7%bb%84)
  - [5.5 集](#55-%e9%9b%86)
  - [5.6 表](#56-%e8%a1%a8)
  - [5.7 Runes](#57-runes)
  - [5.8 符号](#58-%e7%ac%a6%e5%8f%b7)
- [6. 函数](#6-%e5%87%bd%e6%95%b0)
  - [6.1 可选参数](#61-%e5%8f%af%e9%80%89%e5%8f%82%e6%95%b0)
  - [6.2 main() 函数](#62-main-%e5%87%bd%e6%95%b0)
  - [6.3 一等公民函数](#63-%e4%b8%80%e7%ad%89%e5%85%ac%e6%b0%91%e5%87%bd%e6%95%b0)
  - [6.4 匿名函数](#64-%e5%8c%bf%e5%90%8d%e5%87%bd%e6%95%b0)
  - [6.5 作用域](#65-%e4%bd%9c%e7%94%a8%e5%9f%9f)
  - [6.6 词法闭包](#66-%e8%af%8d%e6%b3%95%e9%97%ad%e5%8c%85)
  - [6.7 函数的等价性](#67-%e5%87%bd%e6%95%b0%e7%9a%84%e7%ad%89%e4%bb%b7%e6%80%a7)
  - [6.8 返回值](#68-%e8%bf%94%e5%9b%9e%e5%80%bc)
- [7. 运算符](#7-%e8%bf%90%e7%ae%97%e7%ac%a6)
  - [7.1 算数运算符](#71-%e7%ae%97%e6%95%b0%e8%bf%90%e7%ae%97%e7%ac%a6)
  - [7.2 关系运算法](#72-%e5%85%b3%e7%b3%bb%e8%bf%90%e7%ae%97%e6%b3%95)
  - [7.3 类型推断运算符](#73-%e7%b1%bb%e5%9e%8b%e6%8e%a8%e6%96%ad%e8%bf%90%e7%ae%97%e7%ac%a6)
  - [7.4 赋值运算符](#74-%e8%b5%8b%e5%80%bc%e8%bf%90%e7%ae%97%e7%ac%a6)
  - [7.5 逻辑运算符](#75-%e9%80%bb%e8%be%91%e8%bf%90%e7%ae%97%e7%ac%a6)
  - [7.6 位移运算符](#76-%e4%bd%8d%e7%a7%bb%e8%bf%90%e7%ae%97%e7%ac%a6)
  - [7.7 条件表达式](#77-%e6%9d%a1%e4%bb%b6%e8%a1%a8%e8%be%be%e5%bc%8f)
  - [7.8 多级表示法](#78-%e5%a4%9a%e7%ba%a7%e8%a1%a8%e7%a4%ba%e6%b3%95)
  - [7.9 其它](#79-%e5%85%b6%e5%ae%83)
- [8. 控制语句](#8-%e6%8e%a7%e5%88%b6%e8%af%ad%e5%8f%a5)
  - [8.1 If else](#81-if-else)
  - [8.2 For 循环](#82-for-%e5%be%aa%e7%8e%af)
  - [8.3 While & do-while](#83-while--do-while)
  - [8.4 Break & continue](#84-break--continue)
  - [8.5 Switch case](#85-switch-case)
  - [8.6 断言](#86-%e6%96%ad%e8%a8%80)
- [9. 异常处理](#9-%e5%bc%82%e5%b8%b8%e5%a4%84%e7%90%86)
  - [9.1 Throw](#91-throw)
  - [9.2 Catch](#92-catch)
  - [9.3 Finally](#93-finally)
- [10. 类](#10-%e7%b1%bb)
  - [10.1 使用类成员变量](#101-%e4%bd%bf%e7%94%a8%e7%b1%bb%e6%88%90%e5%91%98%e5%8f%98%e9%87%8f)
  - [10.2 使用构造函数](#102-%e4%bd%bf%e7%94%a8%e6%9e%84%e9%80%a0%e5%87%bd%e6%95%b0)
  - [10.3 获取对象类型](#103-%e8%8e%b7%e5%8f%96%e5%af%b9%e8%b1%a1%e7%b1%bb%e5%9e%8b)
  - [10.4 实例变量](#104-%e5%ae%9e%e4%be%8b%e5%8f%98%e9%87%8f)
  - [10.5 构造函数](#105-%e6%9e%84%e9%80%a0%e5%87%bd%e6%95%b0)
  - [10.6 方法](#106-%e6%96%b9%e6%b3%95)
  - [10.7 抽象类](#107-%e6%8a%bd%e8%b1%a1%e7%b1%bb)
  - [10.8 隐式接口](#108-%e9%9a%90%e5%bc%8f%e6%8e%a5%e5%8f%a3)
  - [10.9 扩展类](#109-%e6%89%a9%e5%b1%95%e7%b1%bb)
  - [10.10 枚举类型](#1010-%e6%9e%9a%e4%b8%be%e7%b1%bb%e5%9e%8b)
  - [10.11 类添加特性](#1011-%e7%b1%bb%e6%b7%bb%e5%8a%a0%e7%89%b9%e6%80%a7)
  - [10.12 类变量和方法](#1012-%e7%b1%bb%e5%8f%98%e9%87%8f%e5%92%8c%e6%96%b9%e6%b3%95)
- [11. 泛型](#11-%e6%b3%9b%e5%9e%8b)
  - [11.1 为什么使用泛型](#111-%e4%b8%ba%e4%bb%80%e4%b9%88%e4%bd%bf%e7%94%a8%e6%b3%9b%e5%9e%8b)
  - [11.2 使用集合字面值](#112-%e4%bd%bf%e7%94%a8%e9%9b%86%e5%90%88%e5%ad%97%e9%9d%a2%e5%80%bc)
  - [11.3 使用带参数化类型的构造函数](#113-%e4%bd%bf%e7%94%a8%e5%b8%a6%e5%8f%82%e6%95%b0%e5%8c%96%e7%b1%bb%e5%9e%8b%e7%9a%84%e6%9e%84%e9%80%a0%e5%87%bd%e6%95%b0)
  - [11.4 泛型集合](#114-%e6%b3%9b%e5%9e%8b%e9%9b%86%e5%90%88)
  - [11.5 泛型约束](#115-%e6%b3%9b%e5%9e%8b%e7%ba%a6%e6%9d%9f)
  - [11.6 使用泛型方法](#116-%e4%bd%bf%e7%94%a8%e6%b3%9b%e5%9e%8b%e6%96%b9%e6%b3%95)
- [12. 库](#12-%e5%ba%93)
  - [12.1 使用库](#121-%e4%bd%bf%e7%94%a8%e5%ba%93)
  - [12.2 实现库](#122-%e5%ae%9e%e7%8e%b0%e5%ba%93)
- [13. 异步](#13-%e5%bc%82%e6%ad%a5)
  - [13.1 处理 Future](#131-%e5%a4%84%e7%90%86-future)
  - [13.2 声明异步函数](#132-%e5%a3%b0%e6%98%8e%e5%bc%82%e6%ad%a5%e5%87%bd%e6%95%b0)
  - [13.3 处理流](#133-%e5%a4%84%e7%90%86%e6%b5%81)
- [14. 生成器](#14-%e7%94%9f%e6%88%90%e5%99%a8)
- [15. 可调用的类](#15-%e5%8f%af%e8%b0%83%e7%94%a8%e7%9a%84%e7%b1%bb)
- [16. 独立性](#16-%e7%8b%ac%e7%ab%8b%e6%80%a7)
- [17. 类型定义](#17-%e7%b1%bb%e5%9e%8b%e5%ae%9a%e4%b9%89)
- [18. 元数据](#18-%e5%85%83%e6%95%b0%e6%8d%ae)
- [19. 注释](#19-%e6%b3%a8%e9%87%8a)
- [20. 小结](#20-%e5%b0%8f%e7%bb%93)


## 1. 一段基础的 Dart 程序
从以下代码片段感受下 Dart 语言的特性：

```Dart
// Define a function.
printIteger(int number) {
    print('The number is $number');
}

// This is where the app starts executing.
main() {
    var number = 42; // Declare and initialize a variable.
    printInteger(number); // Call a function.
}
```
这段程序使用的特性适用于其他所有 Dart 应用：

// This is a comment.<br>
一个单行注释。另外，Dart 也支持多行和文档注视。更多信息看[注释文档](https://dart.dev/guides/language/language-tour#comments)。

int<br>
Dart 自带类型之一，其他的还有 *String*, *List* 和 *bool*。

42<br>
数值字面值，编译时期常量。

print()<br>
打印输出。

'...' 或者 "..."<br>
字符串字面值。

$variableNmae 或者 ${variableName}<br>
字符串差值写法。更多请查看[文档](https://dart.dev/guides/language/language-tour#strings)。

main()<br>
App 执行入口，每个应用必须有。更多信息查看[文档](https://dart.dev/guides/language/language-tour#the-main-function)。

## 2. 重要概念

学习 Dart 过程中，牢记以下概念：<br>
* 任何可以存到变量中的都是对象，每个对象都是类的实例。数值、函数和 `null` 都是对象。所有对象都继承自 [Object](https://api.dart.dev/stable/dart-core/Object-class.html) 类。
* 虽然 Dart 是强类型的，但类型声明是可选的，因为 Dart 有类型推断。上述代码中， `number` 并没有声明类型，被自动推断成 `int`j。可以使用[特定的动态类型](https://dart.dev/guides/language/effective-dart/design#do-annotate-with-object-instead-of-dynamic-to-indicate-any-object-is-allowed)，来声明任意类型的变量。
* Dart 支持泛型，比如 `List<int>` 和 `List<dynamic>`。
* Dart 支持将函数声明在类内部（*实例方法*）和外部（*静态方法*），也支持*嵌套函数*。
* 类似的，Dart 也支持将变量声明在类内部（*实例变量*）和外部（*静态变量*）。实例变量也叫做域(*field*)或属性(*property*)。
* 不同于 Java，Dart 没有 `public`, `protected` 和 `private` 关键字。可以使用 `_` 开头的标识符来表示变量是库内私有的。更多信息请看[文档](https://dart.dev/guides/language/language-tour#libraries-and-visibility)。
* 标识符以字母和下划线开头，后面可以跟字母数字下划线。
* Dart 有表达式(*expressions*)和语句(*statements*)。
* Dart 工具有两种报错类型：*警告*和*错误*。警告表示代码运行结果可能不同于期望，但不会使程序退出。错误分为编译期和运行时。编译器错误会导致程序无法启动，运行时错误会导致程序运行时抛出异常。

## 3. 关键字

|                        |                      |                        |                     |
| :--------------------- | :------------------: | :--------------------: | ------------------: |
| abstract<sup>2</sup>   | dynamic<sup>2</sup>  | implements<sup>2</sup> |    show<sup>1</sup> |
| as<sup>2</sup>         |         else         |   import<sup>2</sup>   |  static<sup>2</sup> |
| assert                 |         enum         |           in           |               super |
| async<sup>1</sup>      |  export<sup>2</sup>  | interface<sup>2</sup>  |              switch |
| await<sup>3</sup>      |       extends        |           is           |    sync<sup>1</sup> |
| break                  | external<sup>2</sup> |  library<sup>2</sup>   |                this |
| case                   | factory<sup>2</sup>  |   mixin<sup>2</sup>    |               throw |
| catch                  |        false         |          new           |                true |
| class                  |        final         |          null          |                 try |
| const                  |       finally        |     on<sup>1</sup>     | typedef<sup>2</sup> |
| continue               |         for          |  operator<sup>2</sup>  |                 var |
| convariant<sup>2</sup> | Function<sup>2</sup> |    part<sup>2</sup>    |                void |
| default                |   get<sup>2</sup>    |        rethrow         |               while |
| deferred<sup>2</sup>   |   hide<sup>1</sup>   |         return         |                with |
| do                     |          if          |    set<sup>2</sup>     |   yield<sup>3</sup> |

尽量避免使用以上关键字作为标识符。如果不可避免需要使用，可以用上角标标记：
* 角标 1 单词是上下文相关的，只有在特定位置才有意义。他们可以在任意位置使用。
* 角标 2 单词是自带标识符。为简化 JS 代码移植到 Dart 的难度，这些关键字不能用作类或者类型的名字以及导入的前缀。
* 角标 3 单词是少有的几个跟异步操作相关的关键字，Dart 1.0 发布后才加入。不能在任何标记 `async`, `async*` 以及 `sync*` 的函数体中使用 `await` 和 `yield` 作为标识符。

剩余的关键字是保留使用的，不能作为标识符。

## 4. 变量

创建并初始化一个变量：
```Dart
var name = 'Bob';
```
变量保存引用，`name` 变量保存对一个 `String` 对象的引用。

`name` 变量推断成 `String` 类型，也可以通过显示声明类型修改。如果对象不是限制为单一类型，可以使用 `Object` 或 `dynamic` 修饰。
```Dart
dynamic name = 'Bob';
```
另一种方式是显示声明类型：
```Dart
String name = 'Bob';
```

### 4.1 默认值

未主动初始化的变量默认初始化为 `null`。即使是数值类型也是如此，在 Dart 的世界里，万物皆对象。
```Dart
int lineCount;
print('${lineCount == null}'); // true
```

### 4.2 Final 和 const 关键字

对于初始化后就不再修改的变量，使用 `final` 或 `const` 替代 `var` 或者类型。final 变量只能设置一次，const 变量是一个编译期常量。一个顶层(top-level)的类变量在第一次使用的时候初始化。

创建并设置一个 final 变量：
```Dart
final name = 'Bab';
final String nickname = 'Bobby';
```
不能修改 final 变量的值：
```Dart
name = 'Alice';
```
使用 `const` 创建**编译期常量**。如果是静态常量，使用 `static const` 修饰。常量必须在声明的时候用字面值或者算术表达式初始化:
```Dart
const bar = 1000000;
const double atm = 1.01325 * bar;
```
`const` 关键字不仅限于声明常量，还可以用于创建常量的值，以及声明构造函数用于创建常量值。任意变量都可以有一个常量值。
```Dart
var foo = const [];
final bar = const [];
const baz = [];
```
当用 `const` 声明一个常量，可以省略初始化表达式中的 `const`。

对于非 const 或 非 final 声明的变量，即使之前存的值是一个常量，仍然可以修改：
```Dart
foo = [1, 2, 3] // 之前是 []
```
但是不能修改一个 const 变量：
```Dart
baz = [42]; // Error
```

## 5. 自带类型

Dart 对以下类型做了特殊支持：
* numbers
* strings
* booleans
* lists
* sets
* maps
* runes(用于在字符串中表达 Unicode 字符)
* symbols

可以用以上任意类型的字面值初始化对象。比如，`this is a string` 是一个字符串字面值，`true` 是一个布尔字面值。

因为 Dart 中的变量都保存一个对象的引用，所以可用构造器（*constructors*)初始化变量。部分自带类型有自己的构造器。比如，用 `Map()` 创建一个表。

### 5.1 数值

Dart 支持两种数值：

int<br>
整型值。

double<br>
64位浮点数。

`int`, `float` 都是 num 子类（subtypes)。num 定义了 +, -, * 和 /，以及 `abs()`, `ceil()` 和 `floor()` 等方法（位运算符定义在 `int`）。其他方法可能定义在 `dart:math` 库中。

整型值是不带小数：
```Dart
var x = 1;
var hex = 0xDEADBEEF;
```
如果数值包含小数，那它就是 double。浮点数字面值：
```Dart
var y = 1.1
var exponents = 1.42e5;
```
字符串和数值相互转换：
```Dart
// String -> int
var one = int.parse('1');
assert(one == 1);

// String -> double
var onePointOne = double.parse('1.1');
assert(onePointOne == 1.1);

// int -> String
String oneAsString= 1.toString();
assert(oneAsString == '1');

// double -> String
String piAsString = 3.14159.toStringAsFixed(2);
assert(piAsString == '3.14');
```

整型的位操作：
```Dart
assert((3 >> 1) == 1);
assert((3 << 1) == 6);
assert((3 | 4) == 7);
```

数值字面值是编译期常量。算术表达式包含的操作数都是编译期常量，那么该表达式也是编译期常量。
```Dart
const msPerSecond = 1000;
const secondsUntilRetry = 5;
const msUntilRetry = secondsUntilRetry * msPerSecond;
```

### 5.2 字符串

Dart 字符串是 UTF-16 单元码的序列。可以用单引号或双引号创建字符串。
```Dart
var s1 = 'Single quotes work well for string literals';
var s2 = "Double quotes work just as well";
var s3 = 'It\'s easy to escape the string delimeter';
var s4 = "It's even easier to use the other delimeter";
```

字符串包含表达式的方式，用 `${expression}`。如果表达式是个标识符，可以省略 {}。
```Dart
var s = 'string interpolation';

assert('Dart has $s, which is very handy.' ==
    'Dart has string interpolation, ' +
        'which is very handy.');
assert('That deserves all caps. ' +
        '${s.toUpperCase()} is very handy!' ==
    'That deserves all caps. ' +
        'STRING INTERPOLATION is very handy!');
```

拼接字符串可以用 `+` 运算符：
```Dart
var s1 = 'String '
    'concatenation'
    " works even over line breaks.";
assert(s1 ==
    'String concatenation works even over '
        'line breaks.');

var s2 = 'The + operator ' + 'works, as well.';
assert(s2 == 'The + operator works, as well.');
```

创建多行字符串的方式：使用 `'''` 或 `"""`：
```Dart
var s1 = '''
You can create
multi-line strings like this one.
''';

var s2 = """This is also a
multi-line string.""";
```

创建原始的字符串方式：使用 `r`：
```Dart
var s = r'In a raw string, not even \n gets special treatment.';
```

字符串字面值是编译期常量：
```Dart
// These work in a const string.
const aConstNum = 0;
const aConstBool = true;
const aConstString = 'a constant string';

// These do NOT work in a const string.
var aNum = 0;
var aBool = true;
var aString = 'a string';
const aConstList = [1, 2, 3];

const validConstString = '$aConstNum $aConstBool $aConstString';
// const invalidConstString = '$aNum $aBool $aString $aConstList';
```

### 5.3 布尔

Dart 用 `bool` 表示布尔值。只有两个对象有布尔类型：布尔字面值 `true` 和 `false`，两者都是编译期常量。

Dart 是类型安全的，意味着 `if (nonbooleanValue)` 或者 `assert (nonbooleanValue)` 是不合法的。应该用显式的值校验：
```Dart
// Check for an empty string.
var fullName = '';
assert(fullName.isEmpty);

// Check for zero.
var hitPoints = 0;
assert(hitPoints <= 0);

// Check for null.
var unicorn;
assert(unicorn == null);

// Check for NaN.
var iMeantToDoThis = 0 / 0;
assert(iMeantToDoThis.isNaN);
```

### 5.4 数组

几乎在所有编程语言中，最通用的集合(collection)是*数组*或者说是对象组。Dart 中，数组是 *List* 对象。

Dart 数组字面值类似 JS。例子：
```Dart
var list = [1, 2, 3];
```

数组索引范围[0, list.length-1]：
```Dart
var list = [1, 2, 3];
assert(list.length == 3);
assert(list[1] == 2);

list[1] = 1;
assert(list[1] == 1);
```

创建编译期常量的数组方法，在数组字面值前加 `const`：
```Dart
var constantList = const [1, 2, 3];
constantList[1] = 1; // Uncommenting this causes an error.
```

Dart 2.3 中引入了 **展开操作符(spread operator(...))** 和 **可空的(null-aware)展开操作符(...?)**，两者都提供了将多个元素插入集合的便捷方法。

如下：
```Dart
var list = [1, 2, 3];
var list2 = [0, ...list];
assert(list2.length == 4);
```

如果展开操作符右边表达式可能为空，可用 `...?` 来避免异常：
```Dart
var list:
var list2 = [0, ...?list];
assert(list2.length == 1);
```

另外，Dart 2.3 还引入了 **collection if** 和 **collection for**，用来构造集合。

**Collection if** 例子：
```Dart
var nav = [
    'Home',
    'Furniture',
    'Plants',
    if (promoActive) 'Outlet'
];
```

**Collection for** 例子：
```Dart
var list1 = [1, 2, 3];
var list2 = [
    '#0',
    for (var i in list1) '#$i'
];
assert(list2[1] == '#1');
```

### 5.5 集

Dart 集无序且元素唯一。Dart 通过两方面支持集，一个是字面值，另一个是 `Set` 类型。

字面值创建集对象：
```Dart
var halogens = {'fluorine', 'chlorine', 'bromine', 'iodine', 'astatine'};
```

创建空集：
```Dart
var set1 = <String>{};
Set<String> set2 = {};
var map = {}; // Create a map, not a set.
```

集添加元素，`add()` 或者 `addAll()`：
```Dart
var set1 = <String>{};
set1.add('fluorine');
set1.addAll(halogens);
```

使用 `.length` 获取集的大小：
```Dart
var set1 = <String>{};
set1.add('fluorine');
set1.addAll(halogens);
assert(set1.length == 5);
```

创建集的编译期字面值，集字面值前加 `const` 关键字：
```Dart
final constantSet = const {
    'fluorine',
  'chlorine',
  'bromine',
  'iodine',
  'astatine',
}
// constantSet.add('helium'); // Uncommenting this causes an error.
```

Dart 2.3 后，集也同数组一样，支持展开操作符和 collection fors 以及 ifs。

### 5.6 表

表包含键值对，键值可以是任意类型的对象。Key 在表中唯一，value 可以重复。Dart 通过两方面支持表，一个是字面值，另一个是 Map 类型。

Dart 表的字面值例子：
```Dart
var gifts = {
  // Key:    Value
  'first': 'partridge',
  'second': 'turtledoves',
  'fifth': 'golden rings'
};

var nobleGases = {
  2: 'helium',
  10: 'neon',
  18: 'argon',
};
```

也可以用构造函数创建的表对象：
```Dart
var gifts = Map();
gifts['first'] = 'partridge';
gifts['second'] = 'turtledoves';
gifts['fifth'] = 'golden rings';

var nobleGases = Map();
nobleGases[2] = 'helium';
nobleGases[10] = 'neon';
nobleGases[18] = 'argon';
```

对已有表中增加键值对：
```Dart
var gifts = {'first': 'partridge'};
gifts['fourth'] = 'calling birds'; // Add a key-value pair
```

从表中获取值：
```Dart
var gifts = {'first': 'partridge'};
assert(gifts['first'] == 'partridge');
```

从表中查不到对应的 key：
```Dart
var gifts = {'first': 'partridge'};
assert(gifts['fifth'] == null);
```

用 `.length` 获取表中键值对数量：
```Dart
var gifts = {'first': 'partridge'};
gifts['fourth'] = 'calling birds';
assert(gifts.length == 2);
```

创建表的编译期常量，表字面值前加 `const` 关键字：
```Dart
final constantMap = const {
  2: 'helium',
  10: 'neon',
  18: 'argon',
};
```

Dart 2.3 后，表也同数组一样，支持展开操作符和 collection fors 以及 ifs。

### 5.7 Runes

Dart runes 是字符串的 UTF-32 码点。

Unicode 为全世界所有字母，数字和符号定义了唯一的数值。由于 Dart 字符串是 UTF-16 单元码的序列，因此在字符串中药表示 32位 Unicode 值需要特殊语法。

通常表达一个 Unicode 码点的形式是 `\uXXXX`，XXXX 是一个4位的16进制数。比如，爱心字符(♥)是 `\u2665`。当指定多于或少于4位数字时，将值放在花括号中。

String 类有一些相关属性获取 rune 信息。比如，`codeUnitAt` 和 `codeUnit` 属性返回16位的单元码，用 `runes` 属性获取字符串中的 runes。

16位和32位转换：
```Dart
main() {
  var clapping = '\u{1f44f}';
  print(clapping);
  print(clapping.codeUnits);
  print(clapping.runes.toList());

  Runes input = new Runes(
      '\u2665  \u{1f605}  \u{1f60e}  \u{1f47b}  \u{1f596}  \u{1f44d}');
  print(new String.fromCharCodes(input));
}
```

### 5.8 符号

*符号* 对象代表 Dart 程序中的运算符或者标识符。你可能从不会用符号，但它们对于按名称引用标识符的 API 非常有用，因为缩小会更改标识符名称而不会更改标识符符号。

获取符号的方法，`#` 号后面跟着标识符：
```Dart
#radix
#bar
```

符号字面值是编译期常量。

## 6. 函数

Dart 是真正的面向对象语言，即使是函数也有类型，*Funtion*。这意味着函数可以赋值给变量或者作为参数传递。还可以调用类的实例，就好像它是一个函数。更多信息查看[文档](https://dart.dev/guides/language/language-tour#callable-classes)。

函数的实现如下：
```Dart
bool isNoble(int atomicNumber) {
    return _nobleGases[atomicNumber] != null;
}
```

虽然类型标注更为高效，但是省略类型的函数依然可用：
```Dart
isNoble(atomicNumber) {
  return _nobleGases[atomicNumber] != null;
}
```

对于只有一个表达式的函数，可以简写为：
```Dart
bool isNoble(int atomicNumber) => _nobleGases[atomicNumber] != null;
```

`=> expr` 语法是 `{ return expr; } 的简写。`=>` 标注通常推断为*箭头*语法。

函数参数支持两种类型：必需(required)和可选(optional)。必需参数在前，可选参数在后。命名为可选的参数仍然可以标记为 `@required`。

### 6.1 可选参数

通过位置或命名中的一种来标记可选参数，但不能两者同时使用。

#### 可选命名参数 <!-- omit in toc -->

调用一个函数，可通过 `paramName: value` 指定命名的参数，比如：
```Dart
enableFlags(bold: true, hidde: false);
```

在定义函数的时候，使用 `{param1, param2, ...}` 指定命名参数：
```Dart
/// Sets the [bold] and [hidden] flags ...
void enableFlags({bool bold, bool hidden}) {...}
```

*Flutter* 实例创建表达式较为复杂，所以 widget 构造函数只使用命名的参数。这能让实例创建表达式可读性更高。

你可以在任意的 Dart 代码中使用 `@required` 来标记命名的参数，从而指定该参数为*必需*参数。举例：
```Dart
const Scrollbar({Key key, @required Widget child});
```

当构造一个 `Scrollbar` 时，如果 `child` 参数缺省，编译器会报错。

*Required* 定义在 *meta* 包中。两种方式导入：import `package:meta/meta.dart` 或导入其它导出 `meta` 的包。

#### 可选位置参数 <!-- omit in toc -->

函数参数列表中，将后面的参数用 `[]` 标记：
```Dart
String say(String from, String msg, [String device]) {
    var result = '$from says $msg';
    if (device != null) {
        result = '$result with a $device';
    }
    return result;
}
```

不带可选参数的调用：
```Dart
assert(say('Bob', 'Howdy') == 'Bob says Howdy');
```

携带可选参数的调用：
```Dart
assert(say('Bob', 'Howdy', 'smoke signal') == 'Bob says Howdy with a smoke signal');
```

#### 默认参数值 <!-- omit in toc -->

函数参数支持给定默认值，包括命名和位置参数。默认值是编译期常量。如果没有主动提供默认值，默认值为 `null`。

默认值例子：
```Dart
/// Sets the [bold] and [hidden] flags ...
void enableFlags({bool bold = false, bool hidden = false}) {...}

// bold will be true; hidden will be false.
enableFlags(bold: true);
```

为位置参数提供默认值：
```Dart
String say(String from, String msg,
    [String device = 'carrier pigeon', String mood]) {
  var result = '$from says $msg';
  if (device != null) {
    result = '$result with a $device';
  }
  if (mood != null) {
    result = '$result (in a $mood mood)';
  }
  return result;
}

assert(say('Bob', 'Howdy') ==
    'Bob says Howdy with a carrier pigeon');
```

函数参数类型为数组或表类型，也支持默认值：
```Dart
void doStuff(
    {List<int> list = const [1, 2, 3],
    Map<String, String> gifts = const {
      'first': 'paper',
      'second': 'cotton',
      'third': 'leather'
    }}) {
  print('list:  $list');
  print('gifts: $gifts');
}
```

### 6.2 main() 函数

每个应用都有一个顶层的 `main()` 函数作为程序入口。该函数返回值为 `void` 并且有一个可选参数，类型为 `List<String>`。

Web 程序的 `main()` 函数例子：
```Dart
void main() {
  querySelector('#sample_text_id');
    ..text = 'Click me!';
    ..onClick.listen(reverseText);
}
```

命令行程序的 `main()` 函数例子：
```Dart
// Run the app like this: dart args.dart 1 test
void main(List<String> arguments) {
  print(arguments);

  assert(arguments.length == 2);
  assert(int.parse(arguments[0]) == 1);
  assert(arguments[1] == 'test');
}
```

用 *args library* 库定义并解析命令行参数。

### 6.3 一等公民函数

函数可以作为其它函数的参数，比如：
```Dart
void printElement(int element) {
  print(element);
}

var list = [1, 2, 3];

// Pass printElement as aparameter.
list.forEach(printElement);
```

函数也可以存到变量中，比如：
```Dart
var loudify = (msg) => '!!! ${msg.toUpperCase()}!!!';
assert(loudify('hello') == '!!!HELLO!!!');
```
上面使用了匿名函数。

### 6.4 匿名函数

大多函数都有名字，比如 `main()` 和 `printElement()`，一些没有名字的函数叫做 *匿名函数(Anonymous funstions)*、*lambda* 或 *闭包(closure)*。函数存到变量中，可以被添加到集合中或者被移除。

匿名函数和一般函数类似，0个或多个参数，参数间用逗号隔开，支持可选类型标注，参数用 `()` 包含。

匿名函数如下：
```Dart
([Type] param1[, ...]) {
  codeBlock;
}
```

以下例子定义一个匿名函数，函数携带一个未定义类型的参数 `item`。每遍历一个 list 中元素，函数都会被调用一次，并打印对应元素的信息。
```Dart
var list = ['apples', 'bananas', 'oranges'];
list.forEach((item) {
  print('${list.indexOf(item)}: $item');
});
```

匿名函数也可以简写成箭头函数。
```Dart
list.forEach((item) => print('${list.indexOf(item)}: $item'));
```

### 6.5 作用域 

Dart 是一种 *lexically scoped language*。代码的布局决定了变量的作用域。

以下例子展示了嵌套函数的变量作用域：
```Dart
bool topLevel = true;

void main() {
  var insideMain = true;

  void myFunction() {
    var insideFunction = true;

    void nestedFunction() {
      var insideNestedFunction = true;

      assert(topLevel);
      assert(insideMain);
      assert(insideFunction);
      assert(insideNestedFunction);
    }
  }
}
```

### 6.6 词法闭包

*闭包* 是函数，能访问作用域内的变量，即使该闭包在原来作用域外部被使用。

函数能延长变量的生命周期。以下例子中，`makeAdder()` 捕获变量 `addBy`。当函数执行结束，`addBy` 被保存到函数中。
```Dart
/// Returns a function that adds [addBy] to the
/// function's argument.
Function makeAdder(num addBy) {
  return (num i) => addBy + i;
}

void main() {
  // Create a function that adds 2.
  var add2 = makeAdder(2);

  // Create a function that adds 4.
  var add4 = makeAdder(4);

  assert(add2(3) == 5);
  assert(add4(3) == 7);
}
```

### 6.7 函数的等价性

以下例子中，比较了顶层函数，静态方法和实例方法的等价性:
```Dart
void foo() {}

class A {
  static void bar() {}
  void baz() {}
}

void main() {
  var x;

  // Comparing top-level functions.
  x = foo;
  print(foo == x);

  // Comparing static methods.
  x = A.bar;
  print(A.bar == x);

  // Comparing instance methods.
  var v = A();
  var w = A();
  var y = w;
  x = w.baz;

  print(y.baz == x);

  print(v.baz != w.baz);
}
```Dart

### 6.8 返回值

所有函数都有返回值。如果没有显示指定，会默认在函数体最后加上 `return null`。
```Dart
foo() {}
print(foo() == null);
```

## 7. 运算符

|          描述          |                    运算符                     |
| :--------------------: | :-------------------------------------------: |
|     一元后缀运算符     |      `expr++`, `expr--`, `()`, `.`, `?.`      |
|     一元前缀运算符     | `-expr`, `!expr`, `~expr`, `++expr`, `--expr` |
| 乘法（multiplicative） |              `*`, `/`, `%`, `~/`              |
|          加法          |                   `+`, `-`                    |
|          位移          |               `<<`, `>>`, `>>>`               |
|          位与          |                      `&`                      |
|         位异或         |                      `^`                      |
|          位或          |                      `|`                      |
|   关系运算和类型推断   |    `>=`, `<=`, `>`, `<`, `as`, `is`, `is!`    |
|          等价          |                  `==`, `!=`                   |
|         逻辑与         |                     `&&`                      |
|         逻辑或         |                     `||`                      |
|        可选判断        |                     `??`                      |
|          条件          |            `expr1 ? expr2 : expr3`            |
|          多级          |                     `..`                      |
|          赋值          | `=`, `*=`, `/=`, `+=`, `-=`, `&=`, `^=`, etc  |

运算符使用例子：
```Dart
a++
a + b
a = b
a == b
c ? a : b
a is T
```

上述表中的运算符优先从高到底排列。运算符优先级的作用：
```Dart
if ((n % i == 0) && (d % i ) == 0) ...
if (n % i == 0 && d % i == 0) ...
```

### 7.1 算数运算符

Dart 支持的算术运算符：
|  运算符 | 意义 |
| ------: | :--- |
|     `+` | 加   |
|     `-` | 减   |
| `-expr` | 负号 |
|     `*` | 乘   |
|     `/` | 除   |
|    `~/` | 取商 |
|     `%` | 取模 |

Dart 支持的递增/递减运算符：
| 运算符  |                  意义                   |
| :-----: | :-------------------------------------: |
| `++var` |  `var = var + 1`(表达式的值是加后的值)  |
| `var++` | `var = var + 1`（表达式的值是加前的值） |
| `--var` | `var = var - 1`（表达式的值是减后的值） |
| `var--` | `var = var - 1`（表达式的值是减前的值） |

### 7.2 关系运算法

| 运算符 |   意义   |
| :----: | :------: |
|  `==`  |   相等   |
|  `!=`  |   不等   |
|  `>`   |   大于   |
|  `<`   |   小于   |
|  `>=`  | 大于等于 |
|  `<=`  | 小于等于 |

### 7.3 类型推断运算符

运行时用于类型校验：
| 运算符 |               意义               |
| :----: | :------------------------------: |
|  `as`  | 类型推断(类型推断错误会抛出异常) |
|  `is`  |    对象是指定类型时返回 true     |
| `is!`  |   对象不是指定类型时返回 true    |

### 7.4 赋值运算符

|      |      |       |       |       |      |
| ---- | ---- | ----- | ----- | ----- | ---- |
| `=`  | `-=` | `/=`  | `%\`  | `>>=` | `^=` |
| `+=` | `*=` | `~/=` | `<<=` | `&=`  | `|=` |

|       | 联合赋值  | 等价表达式  |
| :---: | :-------: | :---------: |
|  op   | `a op= b` | `a= a op b` |
| 例子  | `a += b`  | `a = a + b` |

### 7.5 逻辑运算符

| 运算符  |  意义  |
| :-----: | :----: |
| `!expr` | 逻辑非 |
|  `||`   | 逻辑或 |
|  `&&`   | 逻辑与 |

### 7.6 位移运算符

| 运算符  |            意义            |
| :-----: | :------------------------: |
|   `&`   |            位与            |
|   `|`   |            位或            |
|   `^`   | 位异或（相同为0，不同为1） |
| `~expr` |    位取反（0->1, 1->0）    |
|  `<<`   |          左移一位          |
|  `>>`   |          右移一位          |

### 7.7 条件表达式

Dart 支持两个条件表达式：

`condition ? expr1 : expr2`<br>
如果条件为真，执行表达式1并返回结果；否则，执行表达式2并返回结果。

`expr1 ?? expr2`<br>
如果表达式1非空，返回其值；否则，执行表达式2并返回结果。

### 7.8 多级表示法

连续调用相同对象，使用 `..` 可以简化写法，减少使用临时变量。
```Dart
querySelector('#confirm')
  ..text = 'Confirm'
  ..classes.add('important')
  ..onClick.listen((e) => window.alert('Confirm!'));

// 等价于以下写法
var button = querySelector('#confirm');
button.text = 'Confirm';
button.classes.add('important');
button.onClick.listen((e) => window.alert('Confirmed!'));
```

嵌套写法：
```Dart
final addressBook = (
  AddressBookBuilder()
    ..name = 'jenny'
    ..email = 'jenny@example.com'
    ..phone = (
      PhoneNumberBuilder()
        ..number = 'xxx-xxx-xxxx'
        ..label = 'home'
      .build();
    )
  .build();
)
```

### 7.9 其它

其他运算符：
| 运算符 |         名字         |                  意义                   |
| :----: | :------------------: | :-------------------------------------: |
|  `()`  | Function application |              表示调用函数               |
|  `[]`  |       访问数组       |      引用数组指定索引位置上的元素       |
|  `.`   |     访问成员变量     |             表达式访问属性              |
|  `?.`  |   条件访问成员变量   | 类似 `.`，支持空对象(类似 Swift 可选链) |

## 8. 控制语句

Dart 控制流：
* `if else`
* `switch case`
* `while` & `do-while`
* `break` & `continue`
* `for` 循环
* `assert`

另外，还有 `try-catch` 和 `throw`。

### 8.1 If else

```Dart
if (isRaining()) {
  you.bringRainCoat();
} else if (isSnowing()) {
  you.wearJacket();
} else {
  car.putTopDown();
}
```

不同于 JS 的地方， Dart 条件必须是布尔值。

### 8.2 For 循环

```Dart
var msg = StringBuffer('Dart is fun');
for (var i = 0; i < 5; i++) {
  msg.write('!');
}
```

闭包捕获变量，并在内部拷贝，即使 `i` 改变也不会影响之前的值： 
```Dart
var callbacks = [];
for (var i = 0; i< 2; i++) {
  callbacks.append(() => print(i));
}
callbacks.forEach((c) => c()); // Dart 输出 0, 1； JS 输出 2, 2
```

### 8.3 While & do-while

`while` 在进入循环体之前判断条件：
```Dart
while (!isDone()) {
  doSomething();
}
```

`do-while` 先执行循环体再判断条件：
```Dart
do {
  printLine();
} while(!atEndOfPage())
```

### 8.4 Break & continue

* `break` 跳出循环
* `continue` 跳过当前循环

### 8.5 Switch case

Dart switch 支持整型，字符串和编译期常量。对象必须是相同类型且该类没有重载 `==`。

每个非空的 `case` 从句，必须要有 `break`。其他结束 `case` 的语句：`continue`, `return` 和 `throw`。

非空的 `case` 中省略 `break` 会报编译错误：
```Dart
var command = 'OPEN';
switch (command) {
  case 'OPEN':
  executeOpen();
  // Error: Missing break
  case 'CLOSE':
  executeClose();
  break;
}
```

`case` 可以为空：
```Dart
var command = 'OPEN';
switch (command) {
  case 'OPEN':
  case 'NOW_CLOSED':
  executeNowClosed();
  break;
}
```

Dart 支持 `continue` 加标签的方式控制代码执行：
```Dart
var command = 'CLOSED';
switch (command) {
  case 'CLOSED':
    executeClosed();
    continue nowClosed;
  // Continues executing at the nowClosed label.

  nowClosed:
  case 'NOW_CLOSED':
    // Runs for both CLOSED and NOW_CLOSED.
    executeNowClosed();
    break;
}
```
`case` 内部可以定义局部变量，变量作用域仅限此代码块。

### 8.6 断言

开发者模式下，支持 `assert(condition, optionalMessage)` 终止程序。

## 9. 异常处理

Dart 支持异常捕获机制。异常是程序运行过程中不可知的错误。如果程序没有捕获异常，抛出异常的[**isolate**](https://zhuanlan.zhihu.com/p/40069285) 会被挂起，通常情况下，isolate 和程序都会被终止。

不同于 Java， Dart 的异常都是未经检查的。方法不会声明可能的异常，并且不需要去处理。

Dart 提供了 *Exception*，*Error* 以及其他的子类。开发者可以自定义异常。另外，Dart 程序可以把所有非空对象作为异常抛出。

### 9.1 Throw

抛出异常的例子：
```Dart
throw FormatException('Expected at least 1 section');
```

抛出任意非空对象作为异常：
```Dart
throw 'Out of llamas';
```

因为抛出异常是一个表达式，所以可以出现在任何需要表达式的位置：
```Dart
void distanceTo(Point point) => throw UnimplementedError();
```

### 9.2 Catch

捕获异常能停止异常的传递，给程序处理异常的能力：
```Dart
try {
  breedMoreLlamas();
} on OutOfLlamasException {
  buyMoreLlammas();
}
```

对于能抛出多种异常类型的代码，可以使用多个 catch 从句。
```Dart
try {
  breedMoreLlamas();
} on OutOfLlamasException {
  // A specific exception
  buyMoreLlamas();
} on Exception catch (e) {
  // Anything else that is an exception
  print('Unknown exception: $e');
} catch (e) {
  // No specified type, handles all
  print('Something really unknown: $e');
  }
```

`catch()` 可以指定两个参数，第一个是抛出的异常，第二个是栈回溯([StackTrace](https://api.dart.dev/stable/dart-core/StackTrace-class.html))。
```Dart
try {
  // ···
} on Exception catch (e) {
  print('Exception details:\n $e');
} catch (e, s) {
  print('Exception details:\n $e');
  print('Stack trace:\n $s');
}
```

在当前位置处理异常并继续传递，使用 `rethrow` 关键字：
```Dart
void misbehave() {
  try {
    dynamic foo = true;
    print(foo++); // Runtime error
  } catch (e) {
    print('misbehave() partially handled ${e.runtimeType}.');
    rethrow; // Allow callers to see the exception.
  }
}

void main() {
  try {
    misbehave();
  } catch (e) {
    print('main() finished handling ${e.runtimeType}.');
  }
}
```

### 9.3 Finally

无论是否抛出异常，使用finally子句，确保代码运行。如果 `catch` 没有匹配到异常，该异常会在 `finally` 后继续传播：
```Dart
try {
  breedMoreLlamas();
} finally {
  // Always clean up, even if an exception is thrown.
  cleanLlamaStalls();
}
```

`catch` 匹配到异常后，也会执行 `finally` 从句：
```Dart
try {
  breedMoreLlamas();
} catch (e) {
  print('Error: $e'); // Handle the exception first.
} finally {
  cleanLlamaStalls(); // Then clean up.
}
```

## 10. 类

Dart 是面向对象语言，具有类和基于 mixin 的继承。每个对象都是类的实例，每个类继承自 *Object*。基于 *mixin* 的继承意味着类只有一个超类，但是类的成员可被多个类结构重用。

### 10.1 使用类成员变量

对象的成员由函数和数据组成。当一个方法被调用时，也就是调用对象的某个方法：通过对象的函数和数据获取方法。

使用 `.` 引用实例变量或方法：
```Dart
var p = Point(2, 2);

// Set the value of the instance variable y.
p.y = 3;

// Get the value of y.
assert(p.y == 3);

// Invoke distanceTo() on p.
num distance = p.distanceTo(Point(4, 4));
```

使用 `?.` 避免调用链为 null 时产生异常：
```Dart
// If p is non-null, set its y value to 4.
p?.y = 4;
```

### 10.2 使用构造函数

使用构造器构造对象。构造器命名可以是 `ClassName` 或 `ClassName.identifier`。比如：
```Dart
var p1 = Point(2, 2);
var p2 = Point.fromJson({'x': 1, 'y': 2});
```

以下代码效果相同，构造器前面多一个可选的 `new` 关键字：
```Dart
var p1 = new Point(2, 2);
var p2 = new Point.fromJson({'x': 1, 'y': 2});
```

部分类提供了[常量构造器](https://dart.dev/guides/language/language-tour#constant-constructors)。构造器前加 `const` 修饰，以创建编译期常量：
```Dart
var p = const ImmutablePoint(2, 2);
```

构造两个等价的编译期常量：
```Dart
var a = const ImmutablePoint(1, 1);
var b = const ImmutablePoint(1, 1);

assert(identical(a, b)); // They are the same instance!
```

如果能通过上下文推断出是常量，则可省略 `const`：
```Dart
// Lots of const keywords here.
const pointAndLine = const {
  'point': const [const ImmutablePoint(0, 0)],
  'line': const [const ImmutablePoint(1, 10), const ImmutablePoint(-2, 11)],
};

// 可以简写为：
// Only one const, which establishes the constant context.
const pointAndLine = {
  'point': [ImmutablePoint(0, 0)],
  'line': [ImmutablePoint(1, 10), ImmutablePoint(-2, 11)],
};
```

如果一个常量构造器超出常量上下文，并且没用 `const` 修饰，则创建一个非常量对象：
```Dart
var a = const ImmutablePoint(1, 1); // Creates a constant
var b = ImmutablePoint(1, 1); // Does NOT create a constant

assert(!identical(a, b)); // NOT the same instance!
```

### 10.3 获取对象类型

使用 Object `runtimeType` 属性，在运行时获取对象类型，返回 `Type` 对象：
```Dart
print('The type of a is ${a.runtimeType}');
```
以上内容介绍了如何*使用*类，下面介绍如何实现类。

### 10.4 实例变量

如何声明一个实例变量：
```Dart
class Point {
  num x; // Declare instance variable x, initially null.
  num y; // Declare y, initially null.
  num z = 0; // Declare z, initially 0.
}
```
未初始化的实例变量默认为 `null`。

所以实例变量隐式生成 *getter* 方法。所有实例变量（除了 final）隐式生成 *setter* 方法。
```Dart
class Point {
  num x;
  num y;
}

void main() {
  var point = Point();
  point.x = 4; // Use the setter method for x.
  assert(point.x == 4); // Use the getter method for x.
  assert(point.y == null); // Values default to null.
}
```
关于实例变量的生命周期，实例变量在构造器和初始化器执行之前就已创建，如果声明实例变量的时候手动初始化了，那么初始化也在此时完成。

### 10.5 构造函数

构造器写法：声明一个函数，函数名和类名相同。最常见的构造器形式就是生成构造器，会创建类的一个新实例：
```Dart
class Point {
  num x, y;

  Point(num x, num y) {
    // There's a better way to do this, stay tuned.
    this.x = x;
    this.y = y;
  }
}
```
`this` 关键字引用当前实例。

构造器的一个语法糖写法：
```Dart
class Point {
  num x, y;

  // Syntactic sugar for setting x and y
  // before the constructor body runs.
  Point(this.x, this.y);
}
```

#### 默认构造器 <!-- omit in toc -->

如果没有生命构造器，Dart 会默认生成一个构造器。此构造器没有参数，并调用父类的不带参构造器。

#### 构造器不继承 <!-- omit in toc -->

构造器不支持继承。

#### 带名字的构造器 <!-- omit in toc -->

如果需要创建多个构造器，使用带名字的构造器：
```Dart
class Point {
  num x, y;

  Point(this.x, this.y);

  // Named constructor
  Point.origin() {
    x = 0;
    y = 0;
  }
}
```

#### 调用非默认的父类构造器 <!-- omit in toc -->

默认情况下，子类的构造器调用父类不带名字和参数的构造器，且在子类构造器的头部调用。如果使用了[初始化列表](https://dart.dev/guides/language/language-tour#initializer-list)，此操作会在父类调用前执行。三者顺序：
1. 初始化列表
2. 父类无参构造器
3. 当前类无参构造器


如果父类没有无名无参的构造器，必须手动调用父类的一个构造器。在 `:` 和函数体之间指定父类的构造器。比如：
```Dart
class Person {
  String firstName;

  Person.fromJson(Map data) {
    print('in Person');
  }
}

class Employee extends Person {
  // Person does not have a default constructor;
  // you must call super.fromJson(data).
  Employee.fromJson(Map data) : super.fromJson(data) {
    print('in Employee');
  }
}

main() {
  var emp = new Employee.fromJson({});

  // Prints:
  // in Person
  // in Employee
  if (emp is Person) {
    // Type check
    emp.firstName = 'Bob';
  }
  (emp as Person).firstName = 'Bob';
}
```

#### 初始化列表 <!-- omit in toc -->

除了调用父类构造器外，还可以在构造器函数体之前初始化实例变量。多个初始化之间用逗号分隔：
```Dart
Point.fromJson(Map<String, num> json) : x = json['x'], y = json['y'] {
  print('In Point.fromJson(): ($x, $y)');
}
```

开发模式下，初始化列表中可使用断言：
```Dart
Point.withAssert(this.x, this.y) : assert(x >= 0) {
  print('In Point.withAssert(): ($x, $y)');
}
```

设置 final 字段时，初始化列表较为便利。比如：
```Dart
import 'dart:math';

class Point {
  final num x;
  final num y;
  final num distanceFromOrigin;

  Point(x, y)
      : x = x,
        y = y,
        distanceFromOrigin = sqrt(x * x + y * y);
}

main() {
  var p = new Point(2, 3);
  print(p.distanceFromOrigin);
}
```

#### 重定向构造器 <!-- omit in toc -->

部分构造器的作用只是调用当前类的其它构造器。重定向构造器写法：
```Dart
class Point {
  num x, y;

  Point(this.x, this.y);

  Point.alongzXAxis(num x) : this(x, 0);
}
```

#### 常量构造器 <!-- omit in toc -->

常量构造器用来表示类生成的实例不会改变。用 `const` 修饰构造器且全部实例变量使用 `final`。
```Dart
class ImmutablePoint {
  static final ImmutablePoint origin = const ImmutablePoint(0, 0);

  final num x, y;

  const ImmutablePoint(this.x, this.y);
}
```
常量构造器不一定总是创建常量。更多信息查看[文档](https://dart.dev/guides/language/language-tour#using-constructors)。

#### 工厂构造器 <!-- omit in toc -->

关键字 `factory` 修饰的构造器表示，此构造器不会每次都创建新的实例。比如，工厂构造器可能返回一个缓存中的实例或者子类的实例。

工厂构造器写法：
```Dart
class Logger {
  final String name;
  bool mute = false;

  // _cache is library-private, thanks to
  // the _ in front of its name.
  static final Map<String, Logger> _cache =
      <String, Logger>{};

  factory Logger(String name) {
    if (_cache.containsKey(name)) {
      return _cache[name];
    } else {
      final logger = Logger._internal(name);
      _cache[name] = logger;
      return logger;
    }
  }

  Logger._internal(this.name);

  void log(String msg) {
    if (!mute) print(msg);
  }
}
```

调用工厂构造器同其他构造器方法一样：
```Dart
var logger = Logger('UI');
logger.log('Button clicked');
```

### 10.6 方法

方法是定义在类内部的函数。

#### 实例方法 <!-- omit in toc -->

对象的实例方法内部可访问实例变量和 `this`。例子如下：
```Dart
import 'dart:math';

class Point {
  num x, y;

  Point(this.x, this.y);

  num distanceTo(Point other) {
    var dx = x - other.x;
    var dy = y - other.y;
    return sqrt(dx * dx + dy * dy);
  }
}
```

#### Getters & setters <!-- omit in toc -->

Getters 和 setters 是特殊的方法，能读写对象属性。实例变量默认都有 getter，通常也有 setter。也可用 `get` 和 `set` 自己实现：
```Dart
class Rectangle {
  num left, top, width, height;

  Rectangle(this.left, this.top, this.width, this.height);

  // Define two calculated properties: right and bottom.
  num get right => left + width;
  set right(num value) => left = value - width;
  num get bottom => top + height;
  set bottom(num value) => top = value - height;
}

void main() {
  var rect = Rectangle(3, 4, 20, 15);
  assert(rect.left == 3);
  rect.right = 12;
  assert(rect.left == -8);
}
```

#### 抽象方法 <!-- omit in toc -->

实例方法，getter 和 setter 都能定义为抽象方法，当前类只定义接口，实现交由其它类。抽象方法只能定义在[抽象类](https://dart.dev/guides/language/language-tour#abstract-classes)中。

定义抽象方法，用分号替代函数体：
```Dart
abstract class Doer {
  void soSomething();
}

class EffectiveDoer extends Doer {
  void soSomething() {

  }
}
```

### 10.7 抽象类

关键字 `abstract` 定义*抽象类*（不能被实例化）。抽象类多用于接口定义，实现较多的情况。定义[工厂构造器](https://dart.dev/guides/language/language-tour#factory-constructors)可实例化抽象类。

抽象类通常都有抽象方法，例子如下：
```Dart
// This class is declared abstract and thus
// can't be instantiated.
abstract class AbstractContainer {
  // Define constructors, fields, methods...

  void updateChildren(); // Abstract method.
}
```

### 10.8 隐式接口

类隐式定义了一个接口列表，包括当前类实现的所有成员变量。类 A 在不继承类 B 的情况下，实现类 B 的接口，从而调用类 B 的成员。

声明类的时候用 `implements` 并提供所需的 APIs，从而实现一个或多个接口：
```Dart
class Person {
  final _name;

  Person(this._name);

  String greet(String who) => 'Hello, $who. I am $_name';
}

class Impostor implements Person {
  get _name => '';

  String greet(String who) => 'Hi $who. Do you know who I am?';
}

String greetBob(Person person) => person.greet('Bob');

void main() {
  print(greetBob(Person('Kathy'))); // 'Hello, Bob. I am $Kathy'
  print(geetBob(Impostor())); // 'Hi Bob. Do you know who I am?'
}
```

一个类实现多个接口：
```Dart
class Point implements Comparable, Location {...}
```

### 10.9 扩展类

使用 `extends` 创建子类，`super` 指向父类：
```Dart
class Television {
  void turnOn() {
    _illuminateDisplay();
    _activateIrSensor();
  }
  // ···
}

class SmartTelevision extends Television {
  void turnOn() {
    super.turnOn();
    _bootNetworkInterface();
    _initializeMemory();
    _upgradeApps();
  }
  // ···
}
```

#### 重写成员 <!-- omit in toc -->

子类可重载实例方法、getters 和 setters。`@override` 关键字表示成员被重载：
```Dart
class SmartTelevision extends Television {
  @override
  void turnOn() {...}
  // ···
}
```

#### 可重载运算符 <!-- omit in toc -->

下表中运算符支持重载：
|       |       |       |       |
| :---: | :---: | :---: | :---: |
|  `<`  |  `+`  |  `|`  | `[]`  |
|  `>`  |  `/`  |  `^`  | `[]=` |
| `<=`  | `~/`  |  `&`  |  `~`  |
| `>=`  |  `*`  | `<<`  | `==`  |
|  `-`  |  `%`  | `>>`  |       |

重载 `+`, `-` 运算符：
```Dart
class Vector {
  final int x, y;

  Vector(this.x, this.y);

  Vector operator +(Vector v) => Vector(x + v.x, y + v.y);
  Vector operator -(Vector v) => Vector(x - v.x, y - v.y);
}

void main() {
  final v = Vector(2, 3);
  final w = Vector(2, 2);

  assert(v + w == Vector(4, 5));
  assert(v - w == Vector(0, 1));
}
```

#### noSuchMethod() <!-- omit in toc -->

重载 `noSuchMethod()` 方法，及时处理调用对象不存在的实例变量和方法：
```Dart
class A {
  // Unless you override noSuchMethod, using a
  // non-existent member results in a NoSuchMethodError.
  @override
  void noSuchMethod(Invocation invocation) {
    print('You tried to use a non-existent member: ' +
        '${invocation.memberName}');
  }
}
```

不可调用对象未实现的方法，除非实现以下任意情况：
* 消息接受者有静态类型 `dynamic`
* 接收器有一个定义未实现方法的静态类型（包括抽象类型），接收器的动态类型有一个noSuchMethod（）实现，它与Object类中的实现不同。

### 10.10 枚举类型

枚举表示固定数量的常量值。

#### 用法 <!-- omit in toc -->

使用 `enum` 关键字声明枚举类型：
```Dart
enum Color { red, green, blue }
```

枚举值有个 `index` getter，返回该值在枚举声明中的位置，从 0 开始。第一个值为 0，第二个值为 1...

使用 `values` 在运行时获取所有枚举值：
```Dart
List<Color> colors = Color.values;
assert(colors[2] == Color.blue);
```

枚举在 switch case 中使用：
```Dart
var aColor = Color.red;
switch (aColor) {
  case Color.red:
  print('red');
  break;
  case Color.green:
  print('green');
  break
  default:
  print(aColor);
}
```

枚举类型的局限性：
* 不可子类化，*mix in*，或实现
* 不能显示实例一个枚举类型

### 10.11 类添加特性

Mixins 是一种将类代码共享给其他类的功能。

`with` 关键字*使用* mixin 功能。例子如下：
```Dart
class Musician extends Performer with Musical {

}

class Maestro extends Person with Musical, Aggressive, Demented {
  Maestro(String maestroname) {
    name = maestroName;
    canConduct = true;
  }
}
```

*实现* mixin：创建一个 Object 子类，并且不声明构造器。另外，如果不想该类被当作普通的类，用 `mixin` 关键字代替 `class`。比如：
```Dart
mixin Musical {
  bool canPlayPiano = false;
  bool canCompose = false;
  bool canConduct = false;

  void entertainMe() {
    if (canPlayPiano) {
      print('Playing piano');
    } else if (canConduct) {
      print('Waving hands');
    } else {
      print('Humming to self');
    }
  }
}
```

要指定只有某些类型可以使用mixin，使用 `on` 指定所需的超类：
```Dart
mixin MusicalPerformer on Musician {
  // ... 
}
```

### 10.12 类变量和方法

使用 `static` 关键字创建静态变量和方法。静态方法和变量都是面向类型的，实例无法访问。

#### 静态方法 <!-- omit in toc -->

```Dart
class Queue {
  static const initialCapacity = 16;
}

void main() {
  assert(Queue.initialCapacity == 16);
}
```

静态变量只有在使用时才会被初始化。

#### 静态方法 <!-- omit in toc -->

```Dart
import 'dart:math';

class Point {
  num x, y;
  Point(this.x, this.y);

  static num distanceBetween(Point a, Point b) {
    var dx = a.x - b.x;
    var dy = a.y - b.y;
    return sqrt(dx * dx + dy * dy);
  }
}

void main() {
  var a = Point(2, 2);
  var b = Point(4, 4);
  var distance = Point.distanceBetween(a, b);
  assert(2.8 < distance && distance < 2.9);
  print(distance);
}
```

## 11. 泛型

数组类型声明：`List<E>`，其中 <...> 将类型标记为*泛型*，即，类型内部有个形式上的参数。通常的命名规范，泛型参数名字为单字符，如 E, T, S, K 和 V。

### 11.1 为什么使用泛型

泛型要求代码是类型安全的，但是使用泛型有很多好处：
* 正确使用泛型使代码结构更好
* 减少重复代码

声明一个只含字符串的数组：`List<String>`。
```Dart
var names = List<String>();
names.addAll(['Seth', 'Kathy', 'Lars']);
names.add(42);//编译报错
```

受益于静态分析的前提下，泛型能为多个类型共享一个接口。比如：
```Dart
// 缓存 Object
abstract class ObjectCache {
  Object getByKey(String key);
  void setByKey(String key, Object value);
}

// 缓存 String
abstract class StringCache {
  String getByKey(String key);
  void setByKey(String key, String value);
}

// 使用泛型
abstract class Cache<T> {
  T getByKey(String key);
  void setByKey(String key, T value);
}
```

### 11.2 使用集合字面值

```Dart
var names = <String>['Seth', 'Kathy', 'Lars'];
var uniqueNames = <String>{'Seth', 'Kathy', 'Lars'};
var pages = <String, String>{
  'index.html': 'Homepage',
  'robots.txt': 'Hints for web robots',
  'humans.txt': 'We are people, not machines'
};
```

### 11.3 使用带参数化类型的构造函数

使用构造器时，指定一个或多个类型，类型放在 `<>` 中间。比如：
```Dart
var nameSet = Set<String>.from(names);
```

### 11.4 泛型集合

Dart 泛型类型是*具体化的*，这意味着泛型变量在运行时携带类型信息。例子如下：
```Dart
var names = List<String>();
names.addAll(['Seth', 'Kathy', 'Lars']);
print(names is List<String>); // true
```

### 11.5 泛型约束

当定义泛型，可使用 `extends` 约束泛型：
```Dart
class Foo<T extends SomeBaseClass> {
  String toString() => "Instance of 'Foo<$T>'";
}
class Extender extends SomeBaseClass {}

var someBaseClassFoo = Foo<SomeBaseClass>();
var extenderFoo = Foo<Extender>();
```

不指定泛型参数：
```Dart
var foo = Foo();
print(foo); // Instance of 'Foo<SomeBaseClass>'
```

### 11.6 使用泛型方法

Dart 支持泛型方法或函数：
```Dart
T first<T>(List<T> ts) {
  T tmp = ts[0];
  return tmp;
}
```
上述代码展示了函数泛型参数可使用的位置：
* 函数返回值
* 函数参数
* 内部布局变量

## 12. 库

使用 `import` 和 `library` 指令创建模块化和可共享的代码。库不仅提供 APIs，还是私有的作用域块：下划线开头的标识符仅在库内部可见。每个 Dart 应用都是一个库，即使并不使用 `library` 指令。

库可作为包(package)发布。

### 12.1 使用库

使用 `import`，在一个库中指定另一个库的命名空间。

举个例子，Dart 网页应用通常使用 `dart:html` 库，可以如下导入：
```Dart
import 'dart:html';
```

`import` 指令后面的参数是指向目标库的 URI。对于 Dart 自带的库，使用 `dart:` 作为 sheme。其他库，使用文件路径或 `package:` scheme。包管理工具提供的库使用 `package:` scheme。比如：
```Dart
import 'package:test/test.dart';
```

#### 指定库前缀 <!-- omit in toc -->

当引入的两个库有冲突的标识符，可以为两个库指定前缀，从而避免冲突。例子如下：
```Dart
import 'package:lib1/lib1.dart';
import 'package:lib2/lib2.dart' as lib2;

Element element1 = Element();

lib2.Element element2 = lib2.Element();
```

#### 导入库的部分接口 <!-- omit in toc -->

Dart 支持导入库的部分功能，比如：
```Dart
import 'package:lib1/lib1.dart' show foo;

import 'package:lib2/lib2.dart' hide foo;
```

#### 库懒加载 <!-- omit in toc -->

库的按需加载。以下场景可以使用库按需加载：
* 加快应用启动时间
* A/B test
* 加载较少使用的库

实现懒加载，首先要用 `deferred as` 导入：
```Dart
import 'package:greetings/hello.dart' deferred as hello;
```

需要使用的地方，用库的标识调用 `loadLibrary()`：
```Dart
Future greet() async {
  await hello.loadLibrary();
  hello.printGreeting();
}
```
上述代码中，`await` 关键字会阻塞代码直到库加载完成。更多信息查看[异步操作](https://dart.dev/guides/language/language-tour#asynchrony-support)。

多次调用 `loadLibrary()` 加载同一个库不会出错，且库只会被加载一次。

使用库的懒加载时，记住以下几点：
* 懒加载的库中的常量，只有在懒加载完成后才能作为常量使用
* 不能使用懒加载库中的类型。而应该将接口类型放到第三方库中，让目标库和当前文件共同导入第三方库
* 开发者用 `deferred as namespace` 定义懒加载库的命名空间，Dart 在命名空间后面隐式插入 `loadLibrary()`。`loadLibrary()` 返回 *Future*。

### 12.2 实现库

实现一个库，请查看 [Create Library Package](https://dart.dev/guides/libraries/create-library-packages)：
* 如何组织库的源码
* 如何使用 `export` 指令
* 何时使用 `part` 指令
* 何时使用 `library` 指令

## 13. 异步

Dart 库中有很多返回值为 `Future` 和 `Stream` 的函数。这些函数是异步函数：派发一个耗时任务后直接返回，并不等待任务完成。

`async` 和 `await` 关键字实现异步编程，让异步任务像同步的代码顺序执行。

### 13.1 处理 Future

两种方式处理 Future：
* 使用 `async` 和 `await`
* 使用 Future API，查看 [the library tour](https://dart.dev/guides/libraries/library-tour#future)

`async` 和 `await` 使用：
```Dart
await lookUpVersion();
```

使用 `await` 的代码，必须要写在 *async* 函数内：
```Dart
Future checkVersion() async {
  var version = await lookUpVersion();
}
```

`try`, `catch` 和 `finally` 用于处理 `await` 代码中的错误并执行清理代码：
```Dart
try {
  version = await lookUpVersion();
} catch (e) {
}
```

一个异步函数中，可使用多个 `await`，下述代码中，使用了三个 await 处理任务：
```Dart
var entrypoint = await findEntrypoint();
var exitCode = await runExecutable(entrypoint, args);
await flushThenExit(exitCode);
```

在 `await expr` 中，`expr` 的值通常是 Future，如果不是，系统会自动用 Future 包装。该 Future 对象表示一个会返回对象的 promise。`await expr` 的值就是最终返回的对象。Await 表达式会阻塞代码直到返回最终的对象。

**使用 `await` 的时候报了编译错误，确保 `await` 实在异步函数中。** 比如，想在 `main()` 函数中使用 `await`，那么函数体必须标记为 `async`：
```Dart
Future main() async {
  checkVersion();
  print('In main: version is ${await lookUpVersion()}');
}
```

### 13.2 声明异步函数

异步函数的函数体用 `async` 标记。

为函数添加 `async` 关键字，使得函数返回 Future。如下例子：
```Dart
String lookUpVersion() => '1.0.0';

Future<String> lookUpVersion() async => '1.0.0';
```
从上述代码可知，Dart 自动用 Future 包装返回值。

如果函数没有实际返回值，就返回 `Future<void>`。

### 13.3 处理流

两种方式从流(Stream)中获取值：
* 用 `async` 和 *asynchronous for loop*(`await for`)
* 使用 [Stream API](https://dart.dev/guides/libraries/library-tour#stream)

异步循环格式：
```Dart
await for (varOrType identifier in expression) {

}
```
上述代码中，`expression` 必须是 Stream 类型。代码执行顺序：
1. 等待流释放一个值
2. 变量被赋值为 (1) 释放的值，并执行循环体
3. 重复步骤(1), (2)，直到流被关闭

使用 `break` 或 `return` 停止监听流，执行命令后会跳出循环并对流取消订阅

**当实现一个异步循环的时候，报编译错误，确保 `await for` 代码实在异步函数中。** 比如，在 `main()` 函数中使用异步循环，将 `main()` 函数体标记为 `async`：
```Dart
Future main() async {
  await for (var request in requestServer) {
    handleRequest(request);
  }
}
```

更多异步编程信息，查看 [*dart:async*](https://dart.dev/guides/libraries/library-tour#dartasync---asynchronous-programming)。

## 14. 生成器

用 *生成器函数* 惰性生成一些列值。Dart 自带两种生成器：
* **Synchronous** 生成器：返回一个 [*Iterable*](https://api.dart.dev/stable/dart-core/Iterable-class.html) 对象
* **Asynchronous** 生成器：返回一个 [*Stream*](https://api.dart.dev/stable/dart-async/Stream-class.html) 对象

实现 **synchronous** 生成器函数方法：用 `sync*` 标记函数体，并用 `yield` 语句发送值：
```Dart
Iterable<Int> naturalTo(int n) sync* {
  int k = 0;
  while (k < n) {
    yield k++;
  }
}
```

实现 **asynchronous** 生成器函数方法：用 `async*` 标记函数体，并用 `yield` 发送值：
```Dart
Stream<Int> asynchronousNaturalTo(int n) async* {
  int k = 0;
  while (k < n) {
    yield k++;
  }
}
```

递归生成器，用 `yield*` 改进性能：
```Dart
Iterable<Int> naturalsDownFrom(int n) sync* {
  if (n > 0) {
    yield n;
    yield* naturalsDownFrom(n - 1);
  }
}
```

## 15. 可调用的类

类实现 `call()` 方法后，该类的实例可以像函数一样被调用。

如下例子，`WannabeFunction` 类实现了 call() 函数：
```Dart
class WannabeFunction {
  call(String a, String b, String c) {
    return '$a $b $c!';
  }
}

main() {
  var wf = new WannabeFunction();
  var out = wf('Hi', 'there', 'gang');
  print(out);
}
```

## 16. 独立性

多数计算机包括手机都有多核 CPU。开发者通常用共享内存的线程并发执行程序，以提高 CPU 利用率。然而，共享状态的并发执行更易出错，也使得代码更加复杂。

Dart 用 *isolate* 替代线程。每个 isolate 有自己的堆内存，以确保 isolates 之间不会共享状态。

更多信息查看 [dart:isolate library document](https://api.dart.dev/stable/dart-isolate)。

## 17. 类型定义

Dart 中，函数同字符串和数值一样都是对象。*Typedef* 或者说 *funtion-type alias* 给函数定义个名字，在其它地方使用。类型定义会保留类型信息。

```Dart
class SortedCollection {
  Function compare;

  SortedCollection(Function f) {
    compare = f;
  }
}

int sort(Object a, Object b) => 0;

void main {
  SortedCollection coll = SortedCollection(sort);
  print(coll.compare is Function);
}
```

使用类型定义后：
```Dart
typedef Compare = int Function(Object a, Object b);

class SortedCollection {
  Compare compare;

  SortedCollection(this.compare);
}

int sort(Object a, Object b) => 0;

main {
  SortedCollection coll = SortedCollection(sort);
  print(coll.compare is Function); // true
  print(coll.compare is Compare); // true
}
```

类型定义结合泛型：
```Dart
typedef Compare<T> = int Function(T a, Tb);

int sort(int a, int b) => a - b;

main {
  print(sort is Compare<Int>);
}
```

## 18. 元数据

元数据标注写法：`@` 开头，后跟着编译期常量或者常量构造器。

Dart 中两种标注对所有代码使用: `@deprecated` 和 `override`。
```Dart
class Television {
  @deprecated
  void activate {

  }
}
```

自定义元数据标注：
```Dart
library todo;

class Todo {
  final String who;
  final String what;

  const Todo(this.who, this.what);
}
```
使用自定义的元数据：
```Dart
import 'todo.dart';

@Todo('seth', 'make this do something')
void doSomething() {

}
```
元数据可以出现在以下指令前：库，类，类型定义，类型参数，构造器，工厂方法，字段，参数，变量声明，导入导出。运行时可通过 reflection 获取元数据。

## 19. 注释

Dart 支持单行、多行和文档注释。

## 20. 小结

此文档摘录了 Dart 中较为通用的特性。此外，更多新特性正在开发，尽量兼容当前代码。下一步：[language specification](https://dart.dev/guides/language/spec) 和 [Effective Dart](https://dart.dev/guides/language/effective-dart)。

了解更多关于 Dart 核心库，查看 [A Tour of the Dart Libraries](https://dart.dev/guides/libraries/library-tour)。

