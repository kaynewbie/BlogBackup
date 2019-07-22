---
title: Dart 语言(译)
tags: dart, flutter
---

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
  - [6.5 词法作用域](#65-%e8%af%8d%e6%b3%95%e4%bd%9c%e7%94%a8%e5%9f%9f)
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
  - [10.10 类型的枚举](#1010-%e7%b1%bb%e5%9e%8b%e7%9a%84%e6%9e%9a%e4%b8%be)
  - [10.11 类添加特性](#1011-%e7%b1%bb%e6%b7%bb%e5%8a%a0%e7%89%b9%e6%80%a7)
  - [10.12 类变量和方法](#1012-%e7%b1%bb%e5%8f%98%e9%87%8f%e5%92%8c%e6%96%b9%e6%b3%95)
- [11. 泛型](#11-%e6%b3%9b%e5%9e%8b)
  - [11.1 为什么使用泛型](#111-%e4%b8%ba%e4%bb%80%e4%b9%88%e4%bd%bf%e7%94%a8%e6%b3%9b%e5%9e%8b)
  - [11.2 使用集合字面值](#112-%e4%bd%bf%e7%94%a8%e9%9b%86%e5%90%88%e5%ad%97%e9%9d%a2%e5%80%bc)
  - [11.3 使用带参数化类型的构造函数](#113-%e4%bd%bf%e7%94%a8%e5%b8%a6%e5%8f%82%e6%95%b0%e5%8c%96%e7%b1%bb%e5%9e%8b%e7%9a%84%e6%9e%84%e9%80%a0%e5%87%bd%e6%95%b0)
  - [11.4 泛型集合](#114-%e6%b3%9b%e5%9e%8b%e9%9b%86%e5%90%88)
  - [11.5 限制参数化类型](#115-%e9%99%90%e5%88%b6%e5%8f%82%e6%95%b0%e5%8c%96%e7%b1%bb%e5%9e%8b)
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
  - [19.1 单行注释](#191-%e5%8d%95%e8%a1%8c%e6%b3%a8%e9%87%8a)
  - [19.2 多行注释](#192-%e5%a4%9a%e8%a1%8c%e6%b3%a8%e9%87%8a)
  - [19.3 文档型注释](#193-%e6%96%87%e6%a1%a3%e5%9e%8b%e6%b3%a8%e9%87%8a)
- [20. 小结](#20-%e5%b0%8f%e7%bb%93)

本文列出了 Dart 语言的每个主要功能的用法，从变量和运算符到类库。本文适用于有其他编程语言经验的开发者。
想学习更多 Dart 核心库的，请查看此[文档](https://dart.dev/guides/libraries/library-tour)。想学习更多语言细节的，请查看此[文档](https://dart.dev/guides/language/spec)。

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
* 虽然 Dart 是强类型的，但类型声明是可选的，因为 Dart 有类型推断。上述代码中， `number` 并没有声明类型，被自动推断成 `int。可以使用[特定的动态类型](https://dart.dev/guides/language/effective-dart/design#do-annotate-with-object-instead-of-dynamic-to-indicate-any-object-is-allowed)，来声明任意类型的变量。
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
### 6.3 一等公民函数
### 6.4 匿名函数
### 6.5 词法作用域
### 6.6 词法闭包
### 6.7 函数的等价性
### 6.8 返回值
## 7. 运算符
### 7.1 算数运算符
### 7.2 关系运算法
### 7.3 类型推断运算符
### 7.4 赋值运算符
### 7.5 逻辑运算符
### 7.6 位移运算符
### 7.7 条件表达式
### 7.8 多级表示法
### 7.9 其它
## 8. 控制语句
### 8.1 If else
### 8.2 For 循环
### 8.3 While & do-while
### 8.4 Break & continue
### 8.5 Switch case
### 8.6 断言
## 9. 异常处理
### 9.1 Throw
### 9.2 Catch
### 9.3 Finally
## 10. 类
### 10.1 使用类成员变量
### 10.2 使用构造函数
### 10.3 获取对象类型
### 10.4 实例变量
### 10.5 构造函数
### 10.6 方法
### 10.7 抽象类
### 10.8 隐式接口
### 10.9 扩展类
### 10.10 类型的枚举
### 10.11 类添加特性
### 10.12 类变量和方法
## 11. 泛型
### 11.1 为什么使用泛型
### 11.2 使用集合字面值
### 11.3 使用带参数化类型的构造函数
### 11.4 泛型集合
### 11.5 限制参数化类型
### 11.6 使用泛型方法
## 12. 库
### 12.1 使用库
### 12.2 实现库
## 13. 异步
### 13.1 处理 Future
### 13.2 声明异步函数
### 13.3 处理流
## 14. 生成器
## 15. 可调用的类
## 16. 独立性
## 17. 类型定义
## 18. 元数据
## 19. 注释
### 19.1 单行注释
### 19.2 多行注释
### 19.3 文档型注释
## 20. 小结
