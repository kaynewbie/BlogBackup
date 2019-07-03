# CFRunLoop

名词：Core Foundation, run loop, `sources`, `timers` 和 `observers`
need process:	需要处理	
callout:		调出

`run loop` 对象监听加入到任务中的源，并且当这些源需要处理的时候分发控制。输入源的例子：用户输入，网络连接，周期或者延迟事件，异步回调。
<!-- more -->	
`run loop`监听三种类型的对象：`sources`, `timer`, `observers`。通过**CFRunLoopAddSource**, **CFRunLoopAddTimer**, 或者** CFRunLoopAddObserver**方法把这些对象加入到 `run loop` 中，从而当他们需要处理的时候能够接收回调。如果不想再接受他们的回调，你可以把他们从 `run loop` 中移除。  
每个添加到 `run loop` 中的 `source`, `time`, `observer`都必须关联一个或多个` run loop` 模式。模式决定了一个迭代中需要处理什么事件。`run loop` 每次执行的时候，他都是在指定的模式下工作。当在一个模式中，他指挥处理这个模式中关联的 `sources`, `timers` 和 `observers`。大多数的 `source` 都会被添加到 `run loop` 的默认模式中--这个模式是应用空闲情况下用来处理事件。然而，系统会定义其他的模式，可能执行在这些模式中执行 `run loop` 从而限制哪些已经处理的`sources`, `timers` 和 `observers`。因为 `run loop` 模式都是指定为字符串，你可以自定义模式限制事件的处理。	

`Core Foundation` 定义了一个特殊的模式:**common modes**,你可以关联多个具有**共同指定**的 `sources`, `timers` 和 `observers`的模式。当配置一个对象的时候，使用'kCFRunLoopCommonModes'来指定为common modes。每个run loop都有他自己的common modes，**默认模式总是包含在其中**。用'CFRunLoopAddCommonMode'往集合中添加模式。	
每个线程都必定有一个 `run loop`。你不能创建和销毁一个线程的`run loop`。需要的时候`Core Foundation`会自动为你创建。使用 `CFRunLoopGetCurrent` 获取当前线程的 `run loop`。调用 `CFRunLoopRun` 使当前线程 `run loop` 运行在默认的模式直到调用 `CFRunLoopStop` 停止。你也可以调用 `CFRunLoopRunInMode` 使当前 `run loop` 运行在指定的模式一段时间（或者当 `run loop` 被停止）。一个模式只会当请求的模式有至少一个 `source` 或者 timer to monitor。	
run loop可以递归运行。你可以在任意run loop的调出中调用'CFRunLoopRun or CFRunLoopRunInMode'，并且可以在当前线程的调用栈中创建嵌套的run loop。在一个调出中，你不会被限制在一些可以运行的模式中。你可以创建其他的run loop激活状态，使其运行在任何可以得到的模式，包括调用栈中运行级别更高的模式。	

Cocoa应用基于‘CFRunLoop’自定义实现级别更高的事件循环。



## AFN
### GET
不管是哪种请求方式，内部都调用	

	HTTPRequestOperationWithHTTPMethod:URLString:parameters:success:failure:	

通过这个方法创建'NSMutableURLRequst'对象，再调用

	HTTPRequestOperationWithRequest:success:failure:failure
	
requestSerializer	



# 自动释放池
对象什么时候释放？  
`observer`	两次睡眠之间释放

# 引用策略
Core Foundation

用于'Core Foundation'对象		

Core Foundation的函数命名非常友好。	

*	函数名字中包含**Create**或者**Copy**，你就持有这个对象；如果包含**Get**，那就没有持有对象。