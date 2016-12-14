# LLDB	
2016年8月30日 下午5:49

## 打印
`help`  
`p(print)`用于打印，		
`e(expression)`，修改程序运行时的值		
`p` == `e --`	
`po(print object)`	

`p/<fmt>`,按照格式打印	  
`p/x`(16进制)   
`p/t`(2进制)
<!-- more -->  

## 变量
LLDB可以声明变量，不过都要以`$`开头。
	
```
(lldb) e int $a = 2
(lldb) p $a * 19
38
(lldb) e NSArray *$array = @[ @"Saturday", @"Sunday", @"Monday" ]
(lldb) p [$array count]
2
(lldb) po [[$array objectAtIndex:0] uppercaseString]
SATURDAY
```
返回值类型无法确定的情况，需要声明:

```
(lldb) p (char)[[$array objectAtIndex:$a] characterAtIndex:0]
'M'
(lldb) p/d (char)[[$array objectAtIndex:$a] characterAtIndex:0]
77
```

## 程序流程
*	`c(process continue)`,继续执行
*	`n(next step)`,下一步
*	`s(step in)`,进入函数
*	`thread return <value>`,使用场景：刚进入一个函数，直接模拟返回。

## 断点
### 管理断点
*	`breakpoint(br) list`,断点列表
*	`breakpoint enable`,允许断点
*	`breakpoint disable`,禁止断点

### 创建断点
这个方法创建的断点不会显示在界面上，下次重新运行就没了。

*	`br set -f <filename> -l <line>`	缩写：`br <filename>:<line>`，某文件的某行加断点
*	`br set -F <functionname>`，某个函数加断点

### 断点行为
action 断点中可以执行任意命令：可以是调试器命令，shell 命令，也可以是更直接的打印。	
## 更新UI
渲染服务（backboardd）不同于但前调试进程，所以不会被打断，不需要执行程序就可以更新UI。

```
(lldb) e id $myView = (id)0x7fe3ed101bd0
(lldb) e (void)[$myView setBackgroundColor:[UIColor blueColor]]
(lldb) e (void)[CATransaction flush]
```

## 寻找按钮的action
```
(lldb) po [$myButton allTargets]
{(
    <MagicEventListener: 0x7fb58bd2e240>
)}
(lldb) po [$myButton actionsForTarget:(id)0x7fb58bd2e240 forControlEvent:0]
<__NSArrayM 0x7fb58bd2aa40>(
_handleTap:
)
```

## 寻址
`image lookup --address <address>`

## 常见问题
*	不明类型或者类型不匹配	
error: 'NSLog' has unknown return type; cast the call to its declared return type	
error: 1 errors parsing expression		

需要显示声明类型。		
lldb是不支持宏的。

*	找不到方法		
error: unsupported expression with unknown type		
error: unsupported expression with unknown type		
error: 2 errors parsing expression	
	
LLDB无法通过点语法访问属性，尝试适当改写是否可以通过。

*	Execution was interrupted	
error: Execution was interrupted, reason: EXC_BAD_ACCESS (code=EXC_I386_GPFLT).		
The process has been returned to the state before expression evaluation.		

可能需要显示声明类型。