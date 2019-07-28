---
title: iOS 开发者入坑 Flutter 知识迁移(译)
tags:
  - flutter
  - ios
  - dart
date: 2019-07-28 22:10:33
---


此文档用于帮助 iOS 开发者将现有的 iOS 知识运用到 Flutter 移动应用开发中。如果已经掌握 iOS 框架的基础，能快速通过此篇文章上手 Flutter 开发。

阅读本文前，最好花 15 分钟看完以下关于 [Cupertino](https://www.youtube.com/flutterdev) 的视频。

Flutter 依赖大量的手机操作系统的能力和配置，因此，iOS 技能在开发中会起到很大帮助。Flutter 是一种开发移动 UI 的新方式，但它有额外的插件系统在非 UI 任务上，和操作系统（iOS & Android）交流。iOS 开发专家不需要了解 Flutter 的所有东西。

当运行在 iOS 系统上时，Flutter 已经为此做了一些调整。更多可查看[平台兼容性](https://flutter.dev/docs/resources/platform-adaptations)。

开发过程中，遇到问题时，此文档可作为参考书查看。
<!-- more -->

- [视图](#%e8%a7%86%e5%9b%be)
  - [Flutter 中和 UIView 等价的东西](#flutter-%e4%b8%ad%e5%92%8c-uiview-%e7%ad%89%e4%bb%b7%e7%9a%84%e4%b8%9c%e8%a5%bf)
  - [如何更新 widgets](#%e5%a6%82%e4%bd%95%e6%9b%b4%e6%96%b0-widgets)
  - [widgets 如何布局？如何使用 SB？](#widgets-%e5%a6%82%e4%bd%95%e5%b8%83%e5%b1%80%e5%a6%82%e4%bd%95%e4%bd%bf%e7%94%a8-sb)
  - [如何添加或移除布局中的组件](#%e5%a6%82%e4%bd%95%e6%b7%bb%e5%8a%a0%e6%88%96%e7%a7%bb%e9%99%a4%e5%b8%83%e5%b1%80%e4%b8%ad%e7%9a%84%e7%bb%84%e4%bb%b6)
  - [如何为 widget 添加动画](#%e5%a6%82%e4%bd%95%e4%b8%ba-widget-%e6%b7%bb%e5%8a%a0%e5%8a%a8%e7%94%bb)
  - [如何进行屏幕绘制](#%e5%a6%82%e4%bd%95%e8%bf%9b%e8%a1%8c%e5%b1%8f%e5%b9%95%e7%bb%98%e5%88%b6)
  - [widget 透明度](#widget-%e9%80%8f%e6%98%8e%e5%ba%a6)
  - [如何自定义 widgets](#%e5%a6%82%e4%bd%95%e8%87%aa%e5%ae%9a%e4%b9%89-widgets)
- [导航](#%e5%af%bc%e8%88%aa)
  - [页面导航](#%e9%a1%b5%e9%9d%a2%e5%af%bc%e8%88%aa)
  - [如何导航到其他页面](#%e5%a6%82%e4%bd%95%e5%af%bc%e8%88%aa%e5%88%b0%e5%85%b6%e4%bb%96%e9%a1%b5%e9%9d%a2)
  - [如何返回到 iOS 原生控制器](#%e5%a6%82%e4%bd%95%e8%bf%94%e5%9b%9e%e5%88%b0-ios-%e5%8e%9f%e7%94%9f%e6%8e%a7%e5%88%b6%e5%99%a8)
- [线程和异步操作](#%e7%ba%bf%e7%a8%8b%e5%92%8c%e5%bc%82%e6%ad%a5%e6%93%8d%e4%bd%9c)
  - [如何编写异步代码](#%e5%a6%82%e4%bd%95%e7%bc%96%e5%86%99%e5%bc%82%e6%ad%a5%e4%bb%a3%e7%a0%81)
- [工程结构，本地化，依赖和资源](#%e5%b7%a5%e7%a8%8b%e7%bb%93%e6%9e%84%e6%9c%ac%e5%9c%b0%e5%8c%96%e4%be%9d%e8%b5%96%e5%92%8c%e8%b5%84%e6%ba%90)
  - [Flutter 中如何使用图片资源？如何处理多分辨率？](#flutter-%e4%b8%ad%e5%a6%82%e4%bd%95%e4%bd%bf%e7%94%a8%e5%9b%be%e7%89%87%e8%b5%84%e6%ba%90%e5%a6%82%e4%bd%95%e5%a4%84%e7%90%86%e5%a4%9a%e5%88%86%e8%be%a8%e7%8e%87)
  - [如何存储字符串？如何处理本地化？](#%e5%a6%82%e4%bd%95%e5%ad%98%e5%82%a8%e5%ad%97%e7%ac%a6%e4%b8%b2%e5%a6%82%e4%bd%95%e5%a4%84%e7%90%86%e6%9c%ac%e5%9c%b0%e5%8c%96)
  - [CocoaPods 的替代品？如何添加依赖？](#cocoapods-%e7%9a%84%e6%9b%bf%e4%bb%a3%e5%93%81%e5%a6%82%e4%bd%95%e6%b7%bb%e5%8a%a0%e4%be%9d%e8%b5%96)
- [视图控制器](#%e8%a7%86%e5%9b%be%e6%8e%a7%e5%88%b6%e5%99%a8)
  - [Flutter 中视图控制器的替代品](#flutter-%e4%b8%ad%e8%a7%86%e5%9b%be%e6%8e%a7%e5%88%b6%e5%99%a8%e7%9a%84%e6%9b%bf%e4%bb%a3%e5%93%81)
  - [如何监听 iOS 生命周期事件](#%e5%a6%82%e4%bd%95%e7%9b%91%e5%90%ac-ios-%e7%94%9f%e5%91%bd%e5%91%a8%e6%9c%9f%e4%ba%8b%e4%bb%b6)
- [布局](#%e5%b8%83%e5%b1%80)
  - [Flutter 中 UITableView 和 UICollectionView 的替代品](#flutter-%e4%b8%ad-uitableview-%e5%92%8c-uicollectionview-%e7%9a%84%e6%9b%bf%e4%bb%a3%e5%93%81)
  - [ListView 列表选中](#listview-%e5%88%97%e8%a1%a8%e9%80%89%e4%b8%ad)
  - [如何动态更新 ListView](#%e5%a6%82%e4%bd%95%e5%8a%a8%e6%80%81%e6%9b%b4%e6%96%b0-listview)
  - [ScrollView 替代品](#scrollview-%e6%9b%bf%e4%bb%a3%e5%93%81)
- [手势检测和触摸事件处理](#%e6%89%8b%e5%8a%bf%e6%a3%80%e6%b5%8b%e5%92%8c%e8%a7%a6%e6%91%b8%e4%ba%8b%e4%bb%b6%e5%a4%84%e7%90%86)
  - [如何添加个点击监听](#%e5%a6%82%e4%bd%95%e6%b7%bb%e5%8a%a0%e4%b8%aa%e7%82%b9%e5%87%bb%e7%9b%91%e5%90%ac)
  - [如何 widgets 上的其它事件](#%e5%a6%82%e4%bd%95-widgets-%e4%b8%8a%e7%9a%84%e5%85%b6%e5%ae%83%e4%ba%8b%e4%bb%b6)
- [主题化和文本](#%e4%b8%bb%e9%a2%98%e5%8c%96%e5%92%8c%e6%96%87%e6%9c%ac)
  - [如何为应用创建主题](#%e5%a6%82%e4%bd%95%e4%b8%ba%e5%ba%94%e7%94%a8%e5%88%9b%e5%bb%ba%e4%b8%bb%e9%a2%98)
  - [为 Text 自定义字体](#%e4%b8%ba-text-%e8%87%aa%e5%ae%9a%e4%b9%89%e5%ad%97%e4%bd%93)
  - [自定义 Text 风格](#%e8%87%aa%e5%ae%9a%e4%b9%89-text-%e9%a3%8e%e6%a0%bc)
- [表单输入](#%e8%a1%a8%e5%8d%95%e8%be%93%e5%85%a5)
  - [Flutter 中如何使用表单？如何获取用户输入？](#flutter-%e4%b8%ad%e5%a6%82%e4%bd%95%e4%bd%bf%e7%94%a8%e8%a1%a8%e5%8d%95%e5%a6%82%e4%bd%95%e8%8e%b7%e5%8f%96%e7%94%a8%e6%88%b7%e8%be%93%e5%85%a5)
  - [Text field 占位文字的替代品？](#text-field-%e5%8d%a0%e4%bd%8d%e6%96%87%e5%ad%97%e7%9a%84%e6%9b%bf%e4%bb%a3%e5%93%81)
  - [如何展示校验错误？](#%e5%a6%82%e4%bd%95%e5%b1%95%e7%a4%ba%e6%a0%a1%e9%aa%8c%e9%94%99%e8%af%af)
- [硬件交互，第三方服务和平台](#%e7%a1%ac%e4%bb%b6%e4%ba%a4%e4%ba%92%e7%ac%ac%e4%b8%89%e6%96%b9%e6%9c%8d%e5%8a%a1%e5%92%8c%e5%b9%b3%e5%8f%b0)
  - [如何与平台以及原生代码交互](#%e5%a6%82%e4%bd%95%e4%b8%8e%e5%b9%b3%e5%8f%b0%e4%bb%a5%e5%8f%8a%e5%8e%9f%e7%94%9f%e4%bb%a3%e7%a0%81%e4%ba%a4%e4%ba%92)
  - [如何获取 GPS 感应器？](#%e5%a6%82%e4%bd%95%e8%8e%b7%e5%8f%96-gps-%e6%84%9f%e5%ba%94%e5%99%a8)
  - [如何获取相机？](#%e5%a6%82%e4%bd%95%e8%8e%b7%e5%8f%96%e7%9b%b8%e6%9c%ba)
  - [如何使用 FB 登录？](#%e5%a6%82%e4%bd%95%e4%bd%bf%e7%94%a8-fb-%e7%99%bb%e5%bd%95)
  - [如何使用 Firebase 特性？](#%e5%a6%82%e4%bd%95%e4%bd%bf%e7%94%a8-firebase-%e7%89%b9%e6%80%a7)
  - [如果构建自定义原生集成？](#%e5%a6%82%e6%9e%9c%e6%9e%84%e5%bb%ba%e8%87%aa%e5%ae%9a%e4%b9%89%e5%8e%9f%e7%94%9f%e9%9b%86%e6%88%90)
- [数据库和本地存储](#%e6%95%b0%e6%8d%ae%e5%ba%93%e5%92%8c%e6%9c%ac%e5%9c%b0%e5%ad%98%e5%82%a8)
  - [如何访问 UserDefault？](#%e5%a6%82%e4%bd%95%e8%ae%bf%e9%97%ae-userdefault)
  - [CoreData 的替代品？](#coredata-%e7%9a%84%e6%9b%bf%e4%bb%a3%e5%93%81)
- [调试](#%e8%b0%83%e8%af%95)
  - [Flutter app 调试工具？](#flutter-app-%e8%b0%83%e8%af%95%e5%b7%a5%e5%85%b7)
- [通知推送](#%e9%80%9a%e7%9f%a5%e6%8e%a8%e9%80%81)
  - [如何设置推送消息？](#%e5%a6%82%e4%bd%95%e8%ae%be%e7%bd%ae%e6%8e%a8%e9%80%81%e6%b6%88%e6%81%af)

# 视图
## Flutter 中和 UIView 等价的东西

iOS 中，通常用 `UIView` 创建 UI，且 `UIView` 之间可互相嵌套，以此构成布局。

可粗略地将 Flutter 中的 `Widget` 等价于 `UIView`。Widgets 并不完全匹配 iOS 视图，但当你明白 Flutter 工作原理后，可把它当作声明和构建 UI 的方式。

Widgets 和 `UIView` 的一些不同之处。首先，widgets 声明周期不同：不可变且一直存在，直到需要改变。每当 widgets 或其状态发生变化时，Flutter 框架都会创建一个新的 widget 实例树。相比之下，iOS 视图改变时不会重新创建，重绘的是可变实体（mutable entity），可变实体一旦绘制，只有调用 `setNeedsDisplay()` 重新绘制。

此外，不像 `UIView`，Flutter widgets 是轻量的，部分原因在于它们是不可变的。因为它们本身不是视图，并且不是直接绘制任何东西，而是对 UI 及其语义的描述，这些描述在内部被映射到真正的视图对象上。

Flutter 包含 `Material` 组件库。`Material` 库的 widgets 按照 *Material Desing guidelines* 实现。Material Design 是一个弹性的设计系统，为所有平台做了优化，包括 iOS。

Flutter 有足够的灵活性和便捷性去实现任意设计。iOS 上可使用 `Cupertino widgets` 生成符合 [Apple's iOS design language](https://developer.apple.com/design/resources) 的界面。

## 如何更新 widgets

iOS 上更新视图的方式就是直接修改。Flutter widgets 不可修改且不能直接更新，必须操作 widget 的状态。

Stateful 和 Stateless widgets 概念就是为了修改视图引入。`StatelessWidget` 是没有附属状态的 widget。

当程序描述的界面部分元素不依赖于初始配置意外的任何内容时，`StatelessWidgets` 是非常有用的。

比如，类似 iOS 中，在 `UIImageView` 内放置一张 logo 图片一样。在 Flutter 中，如果 logo 图片不变，可以使用 `StatelessWidget`。

如果想实现一个基于 HTTP 请求动态修改 UI 的场景，使用 `StatefulWidget`。请求完成后，告诉 Flutter 框架 widget `State` 已经更新，框架会自动更新 UI。

Stateful 和 Stateless 最大的区别是，`StatefuleWidgets` 有一个 State 对象，此对象存储状态数据，并在树重构的过程中一直携带。

如果还没理解上述内容，记住以下规则：如果 widget 在 `build()` 方法外改变，那么它就是 stateful。如果 widget 创建后就不改变，它是 stateless。此外，如果一个 widget 是 stateful，它的父 widget 也可能是 stateless。

以下例子展示如何使用 `StatelessWidget`。`Text` 是常见的 `StatelessWidget`。可以查看 `Text` 类型定义，它是 `StatelessWidget` 子类。
```Dart
Text(
'I like Flutter!',
style: TextStyle(fontWeight: FontWeight.bold),
);
```
从上述代码发现， `Text` 并没有携带显式的状态，只靠构造器的参数渲染。

但是，如何动态修改 `Text` 展示文本？

解决上述问题，将 `Text` 包装在一个 `StatefulWidget` 中。
```Dart
class SampleApp extend StatelessWidget {
    @override
    Widget build(BuildContext context) {
        return MaterialApp(
            title: 'Sample App',
            theme: ThemeData(
                primarySwatch: Colors.blue,
            ),
            home: SampleAppPage(),
        );
    }
}

class SampleAppPage extends StatefulWidget {
    SampleAppPage({Key key}) : super(key: key);

    @override
    _SampleAppPageState createState() => _SampleAppPageState();
}

class _SampleAppPageState extends State<SampleAppPage> {

    String textToShow = "I like Flutter";
    void _updateText() {
        setState(() {
            textToShow = "Flutter is Awesome!";
        })
    }

    @override
    Widget build(BuildContext context) {
        return Scaffold(
            appBar: AppBar(
                title: Text("Sample App"),
            ),
            body: Center(child: Text(textToShow)),
            floatingActionButton: FloatingActionButton(
                onPressed: _updateText,
                tooltip: 'Update Text',
                child: Icon(Icons.update),
            ),
        );
    }
}
```

## widgets 如何布局？如何使用 SB？

iOS 支持用 SB 组织视图并设置约束。Flutter 中通过组合 widget 树声明布局。

如下例子展示 widget 那边距：
```Dart
Widget build(BuildContext context) {
    return Scaffold(
        appBar: AppBar(
            title: Text('Sample App'),
        ),
        body: Center(
            child: CupertinoButton(
                onPressed: () {
                    setState(() {
                        _pressedCount++;
                    });
                }
                child: Text('Hello'),
                padding: EdgeInsets.only(left: 10.0, right: 10.0),
            ),
        ),
    );
}
```
任意 widget 都可添加内边距，类似 iOS 中的约束。

在 [widget catalog](https://flutter.dev/docs/development/ui/widgets/layout) 中查看更多 Flutter 布局信息。

## 如何添加或移除布局中的组件

iOS 中，开发者可调用父视图的 `addSubview()` 方法动态增加子视图，也可以调用子视图的 `removeFromSuperview()` 方法动态移除子视图。Flutter 中，widgets 是不可变的，并没有直接等价 `addSubview()` 的方法。

下述例子展示当用户点击按钮时，如何切换两个 widgets：
```Dart
class SampleApp extend StatelessWidget {
    Widget build(BuildContext context) {
        return MaterialApp(
            title: 'Sample App',
            theme: ThemeData(
                primarySwatch: Colors.blue,
            ),
            home: SampleAppPage(),
        );
    }
}

class SampleAppPage extends StatefulWidget {
    SampleAppPage({Key key}) : super(key: key);

    _SampleAppPageState createState() => _SampleAppPageState();
}

class _SampleApppageState extends State<SampleAppPage> {

    bool toggle = true;
    void _toggle() {
        setState(() {
            toggle = !toggle;
        });
    }

    void _getToggleChild() {
        if (toggle) {
            return Text('Toggle on');
        } else {
            return CupertinoButton(
                onPressed: () {},
                child: Text('Toggle Two'),
            );
        }
    }

    Widget build(BuildContext context) {
        return Scaffold(
            appbar: Appbar(
                title: Text('Sample App'),
            ),
            body: Center(
                child: _getToggleChild(),
            ),
            floatingActionButton: FloatingActionButton(
                onPressed: _toggle,
                tooltip: 'Update Text',
                child: Icon(Icons.update),
            ),
        );
    }
}
```

## 如何为 widget 添加动画

iOS 中，调用 UIView `animate(withDuration:animations:)` 方法生成动画。Flutter 中，将 widget 封装到动画库的 widget 中。

Flutter 使用 `Animation<double>` 子类 `AnimationController` 生成动画。`Animation<double>` 可以暂停、查找、终止和反转动画。动画需要一个 `Ticker` 对象，此对象负责在 vsync 发生时发送信令，并在运行时每一帧动画中插入一个 0～1 的线性值。一个控制器可以附带一个或多个 `Animations`。

举个例子，使用 `CurvedAnimation` 实现一个插值曲线动画。按照这种做法，控制器是动画过程主要的数据来源，`CurvedAnimation` 计算曲线并替换控制器的默认线性动态。同 widgets，Flutter 中的动画也是可以组合的。

构建 widget 树时，为其中一个 widget 设置一个动画属性，比如 `FadeTransition` 的透明度，并告诉控制器启动动画。

下述例子展示 FadeTransition 淡出动画：
```Dart
class SampleApp extends StatelessWidget {
    @override
    Widget build(BuildContext) {
        return MaterialApp(
            title: 'Fade Demo',
            theme: ThemeData(
                primarySwatch: Colors.blue,
            ),
            home: MyFadeTest(title: 'Fade Demo'),
        );
    }
}

class MyFadeTest extends StatefulWidget {
    MyFadeTest({Key key, this.title}) : super(key: key);

    final String title;

    @override
    _MyFadeTest createState() => _MyFadeTest();
}

class _MyFadeTest extends State<MyFadeTest> with TickerProviderStateMixin {
    AnimationController controller;
    CurvedAnimation curve;

    @override
    void initState() {
        controller = AnimationController(duration; const Duration(milliseconds: 2000), vsync: this);
        curve = CurvedAnimation(parent: controller, curve: Curves.easeIn);
    }

    Widget build(BuildContext context) {
        return Scaffold(
            appBar: AppBar(
                title: Text(widget.title),
            ),
            body: Center(
                child: Container(
                    FadeTransition(
                        opacity: curve,
                        child: FlutterLogo(
                            size: 100.0,
                        ),
                    ),
                ),
            ),
            floatingActionButton: FloatingActionButton(
                tooltip: 'Fade',
                child: Icon(Icons.brush),
                onPressed: () {
                    controller.forward();
                }
            ),
        );
    }

    @override
    dispose() {
        controller.dispose();
        super.dispose();
    }
}
```

## 如何进行屏幕绘制

iOS 中，开发者用 `CoreGraphics` 绘制线条和形状到屏幕上。Flutter 使用基于 `Canvas` 类的 API 以及两个辅助类(`CustomPaint` 和 `CustomPainter`，后者实现绘制画布的算法)。

Flutter 中，如何实现签名签名画家：
```Dart
class SignaturePainter extends CustomPainter {
    SignaturePainter(this.points);

    final List<Offset> points;

    void paint(Canvas canvas, Size size) {
        var paint = Paint()
            ..color = Colors.black
            ..strokeCap = StrokeCap.round
            ..strokeWidth = 5.0;
        for (int i = 0; i < points.length - 1; i++) {
            if (points[i] != null && points[i + 1] != null) {
                canvas.drawLine(points[i], points[i + 1], paint);
            }
        }
    }

    bool shouldRepaint(SingnaturePainter other) => other.points != points;
}

class Signature extends StatefulWidget {
    SignatureState createState() => SignatureState();
}

class SignatureState extends State<Signature> {
    Widget build(BuildContext context) {
        return GestureDetector(
            onPanUpdate: (DragUpdateDetails details) {
                setState(() {
                    RenderBox refernceBox = context.findRenderObject();
                    Offset localPosition = referencenBox.globalToLocal(details.globalPosition);
                    _points = List.from(_points)
                        ..add(localPosition);
                });
            },
            onPanEnd: (DragDetails details) => _points.add(null),
            child: CustomPaint(painter: SignaturePainter(_points), size: Size.infinite),
        );
    }
}
```

## widget 透明度

iOS 视图都有透明度。Flutter 实现透明度需要使用 Opacity widget。

## 如何自定义 widgets

iOS 中，重载 `UIView` 子类或已存在的视图的方法去自定义视图。Flutter 自定义视图由多个更小的 widget 组合而成。

举例，如何创建一个构造器带一个 label 参数的 `CustomButton`？
```Dart
class CustomButton extends StatelessWidget {
    final String label;

    CustomButton(this.label);

    @override
    Widget build(BuildContext context) {
        return RaisedButton(
            onPressed: () {
            // do something...
        },
        child: Text(label),
        );
    }
}
```

使用 `CustomButton` 时跟其他 widget 一样：
```Dart
@override
Widget build(BuildContext context) {
    return Center(
        child: CustomButton("Hello");
    );
}
```

# 导航
## 页面导航

iOS 页面间转移时，使用 `UINavigationController` 管理视图控制器组成的栈。

Flutter 有类似的实现，`Navigator` 和 `Routes`。`Route` 是页面的抽象，`Navigator` 是管理 routes 的 widget。Route 类比 UIViewController，Navigator 类比 UINavigationController。

页面导航的步骤：
* 构建一个路由表
* 直接导航到指定路由

例子如下：
```Dart
void main() {
    runApp(
        CupertinoApp(
            home: MyAppHome(),
            routes: <String, WidgetBuilder> {
                '/a': (BuildContext context) => MyPage(title: 'page A'),
                '/b': (BuildContext context) => MyPage(title: 'page B'),
                '/c': (BuildContext context) => MyPage(title: 'page C'),
            },
        )
    );
}
```

调用 `Navigator push` 方法，导航到指定路由：
```Dart
Navigator.of(context).pushNamed('/b');
```

`Navigator` 处理路由事件，并得到对应路由结果。对 `push()` 返回值 `Future` 对象使用 `await`。

如下例子，路由到 'location' 页面：
```Dart
Map coordinates = await Navigator.of(context).pushNamed('/location');
```

在 'location' 页内部，`pop()` 时带上结果：
```Dart
Navigator.of(context).pop({"lat":43.821757, "long":-79.226392});
```

## 如何导航到其他页面

iOS 中，用 URL Scheme 跳转指定应用。Flutter 中实现此功能的做法，要么创建原生平台集成，或使用 *existing plugin*，比如 *url_launcher*。

## 如何返回到 iOS 原生控制器

调用 `SystemNavigator.pop()` 相当于以下 iOS 代码的作用：
```Objective-C
UIViewController *viewController = [UIApplication sharedApplication].keyWindow.rootViewController;
if ([viewController isKindOfClass:[UINavigationController class]]) {
    [(UINavigationController *)viewController popViewControllerAnimated: NO];
}
```
如果上述代码不生效，可以创建 [*platform channel*](https://flutter.dev/docs/development/platform-integration/platform-channels) 去调用任意 iOS 代码。

# 线程和异步操作

## 如何编写异步代码

Dart 有一个单线程执行模型，支持 `Isolate`s（一种在其他线程执行 Dart 代码的方式），事件循环和异步编程。Dart 默认运行在主 UI 线程，此线程靠一个事件循环驱动，开发者也可以创建新的 Isolate 去执行代码。Flutter 事件循环等同于 iOS，`Looper` 依附于主线程。

Dart 的单线程模型并不意味着所有内容都作为阻塞操作运行，导致 UI 冻结。相反，使用 Dart 提供的异步工具（比如，`async`/`await`）去执行异步操作。

举例，使用 `async`/`await` 运行网络代码，从而不阻塞 UI，让 Dart 作这些繁重的工作：
```Dart
loadData() async {
    String dataURL = "https://jsonplaceholder.typicode.com/posts";
    http.Response response = await http.get(dataURL);
    setState(() {
        widgets = json.decode(response.body);
    });
}
```

一旦 `await` 完成，调用 `setState()` 更新 UI，此方法会触发 widget 子树的重新构建并更新数据。

如下例子，异步加载数据并展示到 `ListView`：
```Dart
import 'dart:convert';

import 'package:flutter/material.dart';
import 'package:http/http.dart' as http;

void main() {
    runApp(SampleApp());
}

class SampleApp extends StatelessWidget {
    @override
    Widget build(BuildContext context) {
        return MaterialApp(
            title: 'Sample App',
            thme: ThemeData(
                primarySwatch: Colors.blue,
            ),
            home: SampleAppPage(),
        );
    }
}

class SampleAppPage extends StatefulWidget {
    SampleAppPage({Key key}) : super(key: key);
    @override
    _SampleAppPageState createState() => _SampleAppPageState();
}

class _SampleAppPageState extends<SampleAppPage> {
    List widgets = [];

    @override
    void initState() {
        super.initState();
        
        loadData();
    }

    @override
    Widget build(BuildContext context) {
        return Scaffold(
            appBar: AppBar(title: Text("Sample App")),
            body: ListView.builder(
                itemCount: widgets.length,
                itemBuilder: (BuildContext context, int position) {
                    return getRow(position);
                }
            ),
        );
    }
}
```

# 工程结构，本地化，依赖和资源

## Flutter 中如何使用图片资源？如何处理多分辨率？

iOS 中区别对待图片和其它资源，而 Flutter 只有资源这一概念。iOS 中防止在 `Image.xcasset` 目录下的资源，在 Flutter 中，则放在 assets 目录下。同 iOS，assets 目录可以放置任意类型的文件。例如，放置一个 JSON 文件在 `my-assets` 目录下。
```Dart
my-assets/data.json
```

在 `pubspec.yaml` 文件中，声明资源路径：
```Dart
assets:
- my-assets/data.json
```

在代码中，使用 *AssetBundle* 访问资源：
```Dart
import 'dart:async' show Future;
import 'package:flutter/services.dart' show rootBundle;

Future<String> loadString() async {
    return await rootBundle.loadString('my-assets/data.json');
}
```

对于图片，Flutter 同 iOS 一样采用基于屏幕密度的格式。图片资源可能是 `1.0x`, `2.0x`, `3.0x` 或其他任意倍数。*devicePixelRatio* 表示物理分辨率到逻辑分辨率的比例。

资源目录可以放在任意目录下（Flutter 并没有预定义目录结构）。在 `pubspec.yaml` 文件中声明资源，Flutter 就能获取到对应资源。

例如，添加一张 `my_icon.png` 图片，防止在任意目录下（这里命名为 `images`）。将 `1.0x` 倍数图片放在 `images` 一级目录下，将其他倍数图片放置在对应倍数的二级目录下：
```Dart
images/my_icon.png
images/2.0x/my_icon.png
images/3.0x/my_icon.png
```

接着，在 `pubspec.yaml` 文件中声明：
```Dart
assets:
- images/my_icon.png
```

在代码中用 `AssetImage` 访问：
```Dart
return AssetImage("images/my_icon.png");
```

或者直接使用 `Image` widget：
```Dart
@override
Widget build(BuildContext context) {
    return Image.asset("images/my_icon.png");
}
```

更多信息查看 [Adding Assets and Images in Flutter](https://flutter.dev/docs/development/ui/assets-and-images)。

## 如何存储字符串？如何处理本地化？

不同于 iOS 中的 `Localizable.strings`，Flutter 并没有专用的字符串处理系统。目前为止，最好的处理方式是，将字符串声明为类中的静态变量。例如：
```Dart
class Strings {
    static String welcomeMessage = 'Welcome To Flutter';
}
```

如何使用字符串：
```Dart
Text(Strings.welcomeMessage);
```

默认情况下，Flutter 只支持美式英语。如果需要支持其他语言，添加 `flutter_localizations` 库。并且还可能需要添加 Dart *intl* 库，从而使用 i10n 机制，比如日期、时间格式。
```Dart
dependencies:
    flutter_localizations:
        sdk: flutter
    intl: "^0.15.6"
```

如何使用 `flutter_localizations` 例子：
```Dart
MaterialApp(
    localizationsDelegates: [
        GlobalMaterialLocalizations.delegate,
        GlobalWidgetsLocalizations.delegate,
    ],
    supportedLocales: [
        const Locale('en', 'US'), // English
        const Locale('he', 'IL'), // Hebrew
    // ... other locales the app supports
    ],
);
```

`supportedLocales` 指定应用支持的语言，`localizationsDelegates` 保存实际的本地化值。应用使用 `MaterialApp`，`GlobalWidgetsLocalizations` 指定基础的 widgets 本地化值；`MaterialWidgetsLocalizations` 指定 material widgets 值。如果应用使用 `WidgetsApp`，不需要指定后者。除了以上两个代理提供的默认值，还可以自定义本地化值。

当初始化的时候，WidgetsApp(或 MaterialApp) 会根据你提供的 delegates 创建一个 Localizations widget。`Localizations` 可以随时从当前上下文中获取设备的语言，也可使用 `Window.locale`。

通过已知代理的 `Localizations.of()` 方法获取指定的本地化类，从而获取本地化资源。使用 [intl_translation](https://pub.dev/packages/intl_translation) 库提取拷贝出来的信息至 [arb](https://github.com/googlei18n/app-resource-bundle) 文件以供翻译，并用 `intl` 重新将结果导入到应用中以供使用。

想了解 Flutter 中的国际化和本地化详情，查看 [internationalization guide](https://flutter.dev/docs/development/accessibility-and-localization/internationalization)，其中有 intl 和 无 intl 两个版本的样例代码。

在 Flutter 1.0 beta 2 之前，Flutter 资源和原生资源是不可互通的，因为他们在不同的目录下。

## CocoaPods 的替代品？如何添加依赖？

iOS 中，在 `Podfile` 中添加依赖信息。Flutter 使用 Dart 的构建系统和 Pub 包管理来处理依赖。这些工具会将原生 iOS 和 Android 构建任务代理给各自的构建系统。

如果 Flutter 工程中 iOS 目录下使用 CocoaPods，请尽在单独平台需要的情况下，再使用 Podfile 添加依赖。通常情况下，在 `pubspec.yaml` 中声明依赖。[Pub site](https://pub.dev/flutter/packages) 用于查询 Flutter 中可供使用的库。

# 视图控制器

## Flutter 中视图控制器的替代品

iOS 中，用户界面的一部分，通常是一个屏幕或者是一部分。多个控制器组合在一起构建复杂的用户界面，并帮助扩展应用的 UI。Flutter 中，widgets 做了相同的工作。正如导航章节中所说的，Flutter 的屏幕是通过 widgets 展现。使用 `Navigator` 在不同的路由间转移，或者状态的变迁。

## 如何监听 iOS 生命周期事件

iOS 中，重写 `ViewController` 的生命周期方法，以获取视图的生命周期过程，或在 `AppDelegate` 中注册生命周期回调。Flutter 中并没有上述的概念，但可以通过 hook `WidgetsBinding` 观察者以监听事件；还可以监听 `didChangeAppLifecycleState()` 事件。

可观察的生命周期事件：
* `inactive`：应用处于非活跃状态，且不会接受用户输入。此事件仅在 iOS 平台可用，安卓平台并无类似事件
* `paused`：当用当前对用户不可见，并不会响应用户输入，但仍然在后台运行
* `resumed`：应用可见且可接受用户输入
* `suspending`：应用暂时挂起。iOS 并无相同事件。

查看更多关于上述状态的信息，请查看 [AppLifecycleStatus documentation](https://api.flutter.dev/flutter/dart-ui/AppLifecycleState-class.html)。

# 布局

## Flutter 中 UITableView 和 UICollectionView 的替代品

Flutter 中用 `ListView` 替代 `UITableView` 和 `UICollectionView`。

```Dart
import 'package:flutter/material.dart";

void main() {
    runApp(SampleApp());
}

class SampleApp extends StatelessWidget {
    @override
    Widget build(BuildContext build) {
        return MaterialApp(
            title: 'Sample App',
            theme: ThemeData(
                primarySwatch: Colors.blue,
            ),
            home: SampleAppPage(),
        );
    }
}

class SampleAppPage extends StatefulWidget {
    SampleAppPage({Key: key}) : super(key: key);

    @override
    _SampleAppPageState createState() => _SampleAppPageState();
}

class _SampleAppPageState extends State<SampleAppPage> {
    @ovrride
    Widget build(BuildContext build) {
        return Scaffold(
            appBar: AppBar(title: Text("Sample App")),
            body: ListView(children: _getListData()),
        );
    }

    _getListData() {
        List<Widget> widgets = [];
        for (int i = 0; i < 100; i++) {
            widgets.add(Padding(padding: EdgeInsets.all(10, 10, 10, 10), child: Text("Row $i")));
        }
        return widgets;
    }
}
```

## ListView 列表选中

iOS 有 UITableView 的代理方法 `tableView:didSelectRowAtIndexPath:`。Flutter 有手势检测元素 `GestureDetector`：
```Dart
import 'package:flutter/material.dart";

void main() {
    runApp(SampleApp());
}

class SampleApp extends StatelessWidget {
    @override
    Widget build(BuildContext build) {
        return MaterialApp(
            title: 'Sample App',
            theme: ThemeData(
                primarySwatch: Colors.blue,
            ),
            home: SampleAppPage(),
        );
    }
}

class SampleAppPage extends StatefulWidget {
    SampleAppPage({Key: key}) : super(key: key);

    @override
    _SampleAppPageState createState() => _SampleAppPageState();
}

class _SampleAppPageState extends State<SampleAppPage> {
    @ovrride
    Widget build(BuildContext build) {
        return Scaffold(
            appBar: AppBar(title: Text("Sample App")),
            body: ListView(children: _getListData()),
        );
    }

    _getListData() {
        List<Widget> widgets = [];
        for (int i = 0; i < 100; i++) {
            widgets.add(
                GesutreDetector(
                    child: Padding(
                        padding: EdgeInsets.all(10, 10, 10, 10),
                        child: Text("Row $i"),
                    ),
                    onTap: () {
                        print('row tapped');
                    }
                )
            );
        }
        return widgets;
    }
}
```

## 如何动态更新 ListView

iOS 中，更新表视图数据源，并调用对应的 `reloadData` 方法刷新。

Flutter 中，如果你在 `setState()` 内部更行了 widgets，你会发现页面并没有刷新。因为调用 `setState()` 方法后，Flutter 渲染引擎回去检索 widgets 树，比对是否有更新。当检索到 ListView 时，使用 `==` 校验，发现两个 `ListView` 是相等的，于是不会刷新页面。

一个简单更新 `ListView` 的方法：在 `setState()` 内部创建新的 `List`，并将老的数据拷贝到新数组内。虽然这个方法很简单，但是并不推荐在大量数据的情况下使用：
```Dart
import 'package:flutter/material.dart';

void main() {
  runApp(SampleApp());
}

class SampleApp extends StatelessWidget {
  // This widget is the root of your application.
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Sample App',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: SampleAppPage(),
    );
  }
}

class SampleAppPage extends StatefulWidget {
  SampleAppPage({Key key}) : super(key: key);

  @override
  _SampleAppPageState createState() => _SampleAppPageState();
}

class _SampleAppPageState extends State<SampleAppPage> {
  List widgets = [];

  @override
  void initState() {
    super.initState();
    for (int i = 0; i < 100; i++) {
      widgets.add(getRow(i));
    }
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text("Sample App"),
      ),
      body: ListView(children: widgets),
    );
  }

  Widget getRow(int i) {
    return GestureDetector(
      child: Padding(
        padding: EdgeInsets.all(10.0),
        child: Text("Row $i"),
      ),
      onTap: () {
        setState(() {
          widgets = List.from(widgets);
          widgets.add(getRow(widgets.length + 1));
          print('row $i');
        });
      },
    );
  }
}
```

下面推荐一个高效、强大的方法，使用 `ListView.Builder`。当你需要处理动态的数组变化或大数组的时候，这个方法非常好用：
```Dart
import 'package:flutter/material.dart';

void main() {
  runApp(SampleApp());
}

class SampleApp extends StatelessWidget {
  // This widget is the root of your application.
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Sample App',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: SampleAppPage(),
    );
  }
}

class SampleAppPage extends StatefulWidget {
  SampleAppPage({Key key}) : super(key: key);

  @override
  _SampleAppPageState createState() => _SampleAppPageState();
}

class _SampleAppPageState extends State<SampleAppPage> {
  List widgets = [];

  @override
  void initState() {
    super.initState();
    for (int i = 0; i < 100; i++) {
      widgets.add(getRow(i));
    }
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text("Sample App"),
      ),
      body: ListView.builder(
        itemCount: widgets.length,
        itemBuilder: (BuildContext context, int position) {
          return getRow(position);
        },
      ),
    );
  }

  Widget getRow(int i) {
    return GestureDetector(
      child: Padding(
        padding: EdgeInsets.all(10.0),
        child: Text("Row $i"),
      ),
      onTap: () {
        setState(() {
          widgets.add(getRow(widgets.length + 1));
          print('row $i');
        });
      },
    );
  }
}
```

用 `ListView.Builder` 实例替代 ListView 实例，用两个参数初始化：数组初始长度和 `ItemBuilder` 函数。

`ItemBuilder` 函数类似 iOS 中 `cellForRowAt` 方法，携带一个索引，并返回在指定索引要展示的 cell。

最后，最重要的是，`onTap()` 方法内部并不会重新创建一个数组，而是用 `.add` 拼接元素。

## ScrollView 替代品

iOS 中，将元素添加到 `ScrollView` 中，使得用户能滚动视图。

Flutter 中，完成此功能最简单的方式就是用 `ListView`。它既是 `ScrollView` 又是 `TableView`，让你可在竖直方向上布局 widgets：
```Dart
@override
Widget build(BuildContext context) {
    return ListView(
        children: <Widget>[
            Text('Row One'),
            Text('Row Two'),
            Text('Row Three'),
        ],
    );
}
```

更多关于如何布局的信息请查看 [layout tutorial](https://flutter.dev/docs/development/ui/widgets/layout)。

# 手势检测和触摸事件处理

## 如何添加个点击监听

iOS 中，在 view 上添加 `GestureRecognizer` 以处理点击事件。Flutter 中，有两种方法添加触摸监听：
1. 如果 widget 本身支持事件监测，传递一个函数作为参数，在函数内处理事件。例如，`RaisedButton` widget 有一个 `onPressed` 参数：
```Dart
@override
Widget build(BuildContext context) {
    return RaisedButton(
        child: Text('Button'),
        onPressed: () {
            print('Pressed');
        }
    );
}
```

2. 如果 widget 本身并不支持事件监测，将 widget 封装在一个 `GestureDetector` 中，并传一个函数到 `onTap` 参数。
```Dart
class SampleApp extends StatelessWidget {
    @override
    Widget build(BuildContext context) {
        return Scaffold(
            body: Center(
                child: GestureDetector(
                    onTap: () {
                        print('tap');
                    }
                    child: FlutterLogo(
                        size: 200,
                    ),
                ),
            ),
        );
    }
}
```

## 如何 widgets 上的其它事件

使用 `GestureDetector` 可以监听大量手势：
* 单击
    * `onTapDown`：用户在屏幕指定区域点击的操作
    * `onTapUp`：用户在屏幕指定区域抬起的的操作
    * `onTap`：点击发生
    * `onTapCancel`：之前的点击手势没有生效
* 双击
    * `onDoubleTap`：用户在短时间内两次点击同意位置
* 长按
    * `onLongPress`：用户长时间按在屏幕上的一个位置
* 竖直拖动
    * `onVerticalDragStart`：手指在屏幕上并开始竖直滑动
    * `onVerticalDragUpdate`：手指在屏幕上并在竖直方向上滑动一段距离
    * `onVerticalDargEnd`：手指之前在屏幕上竖直滑动并在停止接触前还以一定的速率移动
* 水平拖动
    * `onHorizontalDragStart`：手指放在屏幕上并准备开始水平移动
    * `onHorizontalDargUpdate`：手指在屏幕上并在水平方向上移动一段距离
    * `onHorizontalDragEnd`：手指之前在屏幕上水平移动接着离开屏幕

如下例子展示了 `GestureDetector` 双击事件旋转 Flutter logo：
```Dart
AnimationController controller;
CurvedAnimation curve;

@override
void initState() {
  controller = AnimationController(duration: const Duration(milliseconds: 2000), vsync: this);
  curve = CurvedAnimation(parent: controller, curve: Curves.easeIn);
}

class SampleApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: Center(
        child: GestureDetector(
          child: RotationTransition(
            turns: curve,
            child: FlutterLogo(
              size: 200.0,
            )),
          onDoubleTap: () {
            if (controller.isCompleted) {
              controller.reverse();
            } else {
              controller.forward();
            }
          },
        ),
      ),
    );
  }
}
```

# 主题化和文本

## 如何为应用创建主题

Flutter 对 Material Design 有一个优雅的实现，为开发者提供丰富的风格和主题选项。

为了充分利用 Material 组件的特点，在应用入口处声明 MaterialApp 为顶级 widget。MaterialApp 封装了大量 Material 设计风格的 widget，避免了开发者自己手动实现。它基于 WidgetApp 构建并添加了 Material 指定的功能。

然而，Flutter 仍然足够灵活以实现其他设计风格。iOS 平台可以使用 [Cupertino 库](https://api.flutter.dev/flutter/cupertino/cupertino-library.html)生成符合 [Human Interface Guidelines](https://developer.apple.com/ios/human-interface-guidelines/overview/themes/) 风格的界面。查看此类型的 widgets，查看 [Cupertino widgets gallery](https://flutter.dev/docs/development/ui/widgets/cupertino)。

也可使用 `WidgetApp` 作为顶级 widget，提供了部分 `MaterialApp` 功能。

自定义任意子组件的颜色和风格，给 `MaterialApp` 传一个 `ThemeData` 对象。如下代码，主要的样本设置为蓝色以及文本选中颜色为红色。
```Dart
class SampleApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Sample App',
      theme: ThemeData(
        primarySwatch: Colors.blue,
        textSelectionColor: Colors.red
      ),
      home: SampleAppPage(),
    );
  }
}
```

## 为 Text 自定义字体

iOS 中，在工程导入任意 `ttf` 字体文件，并在 `info.plist` 中创建引用。Flutter 中，做法类似导入图片，将字体文件放置在一个目录下，并在 `pubspec.yaml` 文件中引用。
```Dart
fonts:
   - family: MyCustomFont
     fonts:
       - asset: fonts/MyCustomFont.ttf
       - style: italic
```

代码中，为 `Text` widget 指定字体：
```Dart
@override
Widget build(BuildContext context) {
  return Scaffold(
    appBar: AppBar(
      title: Text("Sample App"),
    ),
    body: Center(
      child: Text(
        'This is a custom font text',
        style: TextStyle(fontFamily: 'MyCustomFont'),
      ),
    ),
  );
}
```

## 自定义 Text 风格

和字体一样，你也可以为 `Text` 自定义其它元素风格。`Text` 有一个风格参数，携带 `TextStyle` 对象，你可以在此对象中自定义大量参数：
* `color`
* `decoration`
* `decorationColor`
* `decorationStyle`
* `fontFamily`
* `fontSize`
* `fontStyle`
* `fontWeight`
* `hashCode`
* `height`
* `inherit`
* `letterSpacing`
* `textBaseline`
* `wordSpacing`

# 表单输入

## Flutter 中如何使用表单？如何获取用户输入？

Flutter 中有用于处理表单的特殊 widgets。如果使用 `TextField` 或 `TextFormField`，可以指定 [TextEditingController](https://api.flutter.dev/flutter/widgets/TextEditingController-class.html) 去获取用户输入：
```Dart
class _MyFormState extends State<MyForm> {
  // Create a text controller and use it to retrieve the current value.
  // of the TextField!
  final myController = TextEditingController();

  @override
  void dispose() {
    // Clean up the controller when disposing of the Widget.
    myController.dispose();
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Retrieve Text Input'),
      ),
      body: Padding(
        padding: const EdgeInsets.all(16.0),
        child: TextField(
          controller: myController,
        ),
      ),
      floatingActionButton: FloatingActionButton(
        // When the user presses the button, show an alert dialog with the
        // text the user has typed into our text field.
        onPressed: () {
          return showDialog(
            context: context,
            builder: (context) {
              return AlertDialog(
                // Retrieve the text the user has typed in using our
                // TextEditingController
                content: Text(myController.text),
              );
            },
          );
        },
        tooltip: 'Show me the value!',
        child: Icon(Icons.text_fields),
      ),
    );
  }
}
```

你可以在 [Flutter Cookbook](https://flutter.dev/docs/cookbook) 中的 [Retrieve the value of a text field](https://flutter.dev/docs/cookbook/forms/retrieve-input) 中查看更多信息以及全部代码。

## Text field 占位文字的替代品？

Flutter 中，为 `Text` widget 提供一个 `InputDecoration` 对象作为构造器 decoration 参数，以实现占位文本的效果。
```Dart
body: Center(
  child: TextField(
    decoration: InputDecoration(hintText: "This is a hint"),
  ),
)
```

## 如何展示校验错误？

同构造器参数 decoration 中提供 “hint” 一样。

然而，你不会想要刚开始就显示错误，而是，当用户输入非法数据时，更细状态，把那个传入一个新的 `Inputdecoration` 对象。
```Dart
class SampleApp extends StatelessWidget {
  // This widget is the root of your application.
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Sample App',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: SampleAppPage(),
    );
  }
}

class SampleAppPage extends StatefulWidget {
  SampleAppPage({Key key}) : super(key: key);

  @override
  _SampleAppPageState createState() => _SampleAppPageState();
}

class _SampleAppPageState extends State<SampleAppPage> {
  String _errorText;

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text("Sample App"),
      ),
      body: Center(
        child: TextField(
          onSubmitted: (String text) {
            setState(() {
              if (!isEmail(text)) {
                _errorText = 'Error: This is not an email';
              } else {
                _errorText = null;
              }
            });
          },
          decoration: InputDecoration(hintText: "This is a hint", errorText: _getErrorText()),
        ),
      ),
    );
  }

  _getErrorText() {
    return _errorText;
  }

  bool isEmail(String emailString) {
    String emailRegexp =
        r'^(([^<>()[\]\\.,;:\s@\"]+(\.[^<>()[\]\\.,;:\s@\"]+)*)|(\".+\"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$';

    RegExp regExp = RegExp(emailRegexp);

    return regExp.hasMatch(emailString);
  }
}
```

# 硬件交互，第三方服务和平台

## 如何与平台以及原生代码交互

Flutter 并不直接在平台上运行代码，而是直接用 Dart 代码原生运行在设备上，绕过平台指定的 SDK 限制。例如，当你用 Dart 发起一个网络请求，该请求直接运行在 Dart 上下文。而不是调用 iOS 或 Android 的 API。你的 Flutter 应用仍然被原生平台的 `ViewController` 作为一个视图管理，但并不直接访问 `ViewController` 或者原生框架。

这并不意味着 Flutter 应用不能与原生 API 或原生代码交互。Flutter 提供 platform channels 和宿主 `ViewController` 互相交流及交换数据。Platform channels 实质上是异步消息机制，以桥接 Dart 代码和宿主 `ViewController`。开发者可以使用 platform channels 在原生端执行方法，或者从设备感应器获取数据。

除了直接使用 platform channels，也可使用预先定义的[插件](https://flutter.dev/docs/development/packages-and-plugins/using-packages)（为某个目标封装的原生和 Dart 代码）。例如，Flutter 中直接用插件获取相册和设备相机，而不需要编写集成代码。[Pub site](https://pub.dev/) 提供查找插件，Dart 和 Flutter 开源库。一些库可能只支持一个平台或多个平台。

如果在 Pub 上找不到满足需求的插件，可[自行编写](https://flutter.dev/docs/development/packages-and-plugins/developing-packages)并[发布到 Pub](https://flutter.dev/docs/development/packages-and-plugins/developing-packages#publish)。

## 如何获取 GPS 感应器？

使用 [deolocator](https://pub.dev/packages/geolocator) 社区插件。

## 如何获取相机？

[image_picker](https://pub.dev/packages/image_picker) 是使用广泛的获取相机插件。

## 如何使用 FB 登录？

使用 [flutter_facebook_login](https://pub.dev/packages/flutter_facebook_login) 集成 FB 登录。

## 如何使用 Firebase 特性？

[First party plugins](https://pub.dev/flutter/packages?q=firebase) 包含了大多数 Firebase 功能。这些插件是 Flutter 团队开发维护。

## 如果构建自定义原生集成？

[自行开发库或插件](https://flutter.dev/docs/development/packages-and-plugins/developing-packages)。

Flutter 插件架构类似 Android 的 Event bus：发送一个消息，并让接受者处理然后发挥一个结果。此时，接受者运行消息在 iOS 或 Android 原生。

# 数据库和本地存储

## 如何访问 UserDefault？

iOS 中，`UserDefault` 用于保存多个键值对到属性列表文件中。

Flutter 中，使用 [Shared Preferences plugin](https://pub.dev/packages/shared_preferences) 获取相同的功能。此插件封装了 iOS 的 `UserDefault` 和 Android 的 `SharedPreferences`。

## CoreData 的替代品？

iOS 中，使用 CoreData 存储结构化数据。这是基于 SQL 数据库的一层封装，使得较为容易地进行和模型相关的查询。

Flutter 中，用 [SQFlite](https://pub.dev/packages/sqflite) 插件获取此功能。

# 调试

## Flutter app 调试工具？

使用 DevTools 套件调试 Flutter 或 Dart 应用。

DevTools 支持 profiling，检查堆栈，检视 widget 树，记录诊断日志，调试，观察代码执行行数，调试内存泄露和内存碎片等。更多信息查看 [DevTools](https://flutter.dev/docs/development/tools/devtools) 文档。

# 通知推送

## 如何设置推送消息？

iOS 需要在开发者中心注册应用。

Flutter 中，使用 `firebase_messaging` 插件获取推送功能。

关于 Firebase Cloud Messaging API 查看 [firebase_messageing](https://pub.dev/packages/firebase_messaging) 插件文档。
