# KIF 文档
  
>  **原文地址：**[https://github.com/kif-framework/KIF](https://github.com/kif-framework/KIF).  
>  **KIF文档地址：**[http://cocoadocs.org/docsets/KIF/2.0.0/index.html](http://cocoadocs.org/docsets/KIF/2.0.0/index.html)
<!-- more -->

## 1.KIF介绍
* 关键类： **KIFTestCase**是**XCTestCase**的子类、**KIFUITestActor**
* 主要方法：     

```  
case类: beforeEach, afterEach, testXXXX;
actor类: tapViewWithAccessibilityLabel:, waitForViewWithAccessibilityLabel:,
在代码中设置: setAccessibilityLabel:, setIsAccessibilityElement:;
switch: setOn: forSwitchWithAccessibilityLabel:  
```		    

## 2.KIF集成（使用cocoapods）

* 创建项目，不勾选 `include Unit Test` 和 `include UI Test`(勾选怎么操作？)；  
* 导航目录选中项目，然后在target左下角点击加号(区别于窗口左下角的加号)，选中`unit bundle`，命名确定；  
* 导航目录下生成target，其中`.m`文件，将其删除(因为我们要使用KIF);  
* 创建podfile，内容如下，保存退出，`pod install`，编辑，完成  

```
target 'Acceptance Tests', :exclusive => true do 
pod 'KIF', '~> 3.0', :configurations => ['Debug']  
end
```  

## 3.KIF使用 

* 选中项目,再选中你刚创建的target->Build Phases->Target Dependencies，点+，选中响应target；  
* Build Setting->Linking->Bundle Loader,写入`$(BUILT_PRODUCTS_DIR)/你的项目名字.app/你的项目名字`；  
* Build Setting->Testing->Test Host,写入`$(BUNDLE_LOADER)`，搜索`Wrapper Extension`，确认对应`xctest`

###	使用方法  
* 测试target中，创建KIFTestCase的子类，.m中实现`beforeEach`(数据初始化)，测试方法(`testXXXX`，编译器会自动检测到并执行)
* 测试方法中，`[tester tapViewWithAccessibilityLabel:]`主要是这个方法，其他有些不同控件方法不一样,(switch,alertController,etc)
* 切换视图控制器，要用`waitForViewWithAccessibilityLabel:`保证视图控制器已经出现

## 4.常见问题
* cocoapods头文件找不到?	
`build setting`下`User Header Search Paths`(区别于`Header Search Paths`)，写入`${SRCROOT}`,选择`recursive`	
* 模拟器加载但是应用没有出现，加载10秒超时  
检查`Test Host`设置是否正确
* 测试方法超时，view not found
视图设置`accessibility label`。xib中设置步骤: `inspector`第三个，`accessibility`组中的`Label`

