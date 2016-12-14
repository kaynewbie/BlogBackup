# Concurrency Programming Guide

为了提高CPU计算能力，增加芯片核心数，为了让应用更充分利用CPU，应用使用多线程


## operation queues

*	nsoperation					基类

通常要加到operation queues中执行(oq并不是直接执行，而是由其他线程执行或者通过gcd);
如果不加到operation queues，可以直接调用`start`。手动执行operation会让代码负担更重，因为一个没有就绪的operation调用`start`就会发出异常。
<!-- more -->

**依赖**		
设置依赖是一个很方便的确定operation执行顺序的方法。`addDependency:`,`removeDependency:`。只有依赖执行完了，这个operation才能进入就绪状态。	
不管依赖是否执行成功，对原来的operation无影响。一个operation的依赖被取消或者执行失败，
由你来决定是否执行这个operation，这需要你让operation结合一些错误追踪的能力。

**键值观察属性**		
isCancelled - read-only		
isAsynchronous - read-only	
isExecuting - read-only		
isFinished - read-only		
isReady - read-only		
dependencies - read-only	
queuePriority - readable and writable	
completionBlock - readable and writable		
虽然可以讲观察者绑定在这些属性，但不应该和**视图**元素绑定，因为关于视图的代码要在**主线程**执行，operation可以在任何线程执行，和这些operation绑定的KVO通知也会在任何线程执行。

**多线程注意**		
nsoperation子类，实现一些`accessors`，要注意线程同步。

**异步VS同步**

**方法重写**
不并发的operation，只需要重写`main`，可能有数据，如果实现了`settter`,`getter`，要保证线程安全;并发的operation，至少实现这些方法或属性`start`,`asynchronous`,`executing`,`finished`。
`start`负责让operation在异步方式运行,开线程或调用异步函数，并且更新执行状态;通过`executing`属性报告,通过发送通知，让感兴趣的知道，这个属性需要线程安全;

**cancel命令**	
cancel不会立即强行停止operation。所有的operations都认可`cancelled`属性，你可以在代码中判断。**NOTE**:一个线程是否被加入到队列中决定了`cancel`的行为。未加入，这个方法会将operation标记成**已完成**；已加入，将operation标记成**就绪**，并立刻调`start`,然后退出，operation从队列中清楚。	
主要代码要周期性地检查`cancelled`属性。实现`start`方法，应该早点检查是否取消然后再决定怎么做。	

**执行operation**		
`start`: 更新执行状态，并调用`main`；手动执行operation才调用这个方法。	
`main`: 实现这个方法，不要调`super`。自动执行在nsoperation提供的自动释放池，所以不需要手动创建。并发operation不需要实现这个方法。		
`cancel`: 这个方法会更新状态，但不会强制停止你的operation。如果已经执行结束，不会有影响。如果一些已经添加到队列，但还没执行operation，可以将其更快地移出队列。
如果operation已经加入队列，并且等待其他依赖operation完成时，这些operation之后会被忽略。队列会很快调用这个operation的`start`，并将它移出队列。

*	nsblockoperation	

一个对象可以管理一个或多个代码块。当管理多个代码块时，只有所有代码块完成，这个operation才会完成。	
添加了代码块的operation是按默认优先级添加到队列中。这些代码块本身不会获得任何执行环境的配置。		
operation正在执行或已经执行结束的时候调用`addExecutionBlock:`会抛出异常。

初始化至少添加一个代码块。当要执行一个`nsblockoperation`时，他会将所有的代码块按照默认优先级提交到并行分发队列。这个operation是在一个单独线程中执行，

*	nsinvocationoperation

管理一个方法封装的单个任务。这个类实习了一个非并发的operation。

```
- (instancetype)initWithTarget:(id)target
                      selector:(SEL)sel
                        object:(id)arg   
sel:可以有0或1个参数。如果有参数，参数类型必须是id；返回值可以是void，纯量值或者id。operation执行结束后，可以在result中访问返回值。
                  
```

`- (instancetype)initWithInvocation:(NSInvocation *)inv`inv会对他的参数引用计数加一。
可以通过查看result属性，看是否有异常。

使用情况：你调用的方法会根据环境改变。例如，根据用户的动态输入选择方法执行。


**自定义operation**	
自定义非并行operation只需要响应`主任务`和`取消`；并行operation则需要重写更多代码。

---	
无论什么operation，都要在创建之后，添加到队列中之前，进行配置。	
多个依赖不能在同一个队列中运算。两个operation不能相互设置为对方的依赖。	
**优先级**	
添加到队列中的operation的执行顺序，**首先**是根据operation的就绪状态；**然后**是根据优先级。	
通过`setQueuePriority: `改变优先级。	
优先级只使用在同一队列中的operation。不同队列确定各自的优先级，所以这就会出现不同队列，低优先级的operation比高优先级的先执行。	

如果你想要拿到执行完的结果，需要对operation保持引用，因为你没有机会再从队列中获取。队列会迅速执行完operation，然后将其移除。

**执行**	
通常队列都会很快执行加入队列的operation，但有几个原因会导致延迟执行加入队列的operation。1.operation依赖还未执行完成的operation；2.队列被挂起或者已经执行最大数量的operation。

** IMPROTANT **		
不要修改已经添加到队列中的operation。因为operation在队列中等待的时候，它可能随时会被执行，修改配置可能会产生不好的影响。

虽然队列是为了并发执行设计的，但是它也可以强制队列一个时间只执行一个operation(`setMaxConcurrentOperationCount:`)。虽然可以达到串行的效果，但是执行顺序还是根据就绪状态和优先级决定的。所以，这个串行表现比不上GCD中的串行队列。如果你对顺序由要求，那你应该在operation进入队列前，设置依赖。

** 手动执行 **	
手动执行要确保operation处于就绪状态，并且调用`start`。`start`会多次检查状态。如果你的operation被取消或者没有处于就绪状态而抛出异常，它就会避免执行。	
如果定义了一个并发的operation，应该最开始判断`isConcurrent `，如果返回`NO`，确保能决定是否重开一条线程。


## dispatch queues

## dispatch sources