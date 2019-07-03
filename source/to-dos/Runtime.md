# Runtime  

简称运行时，是系统在运行时候的一些机制，其中最主要的是消息机制。
`[obj someMethod]`  --> `objc_msgSend(obj, @selector(someMethod))`

<!-- more -->

### 相关问题

1.头文件
	*runtime
2.用在哪里
	*NSCoding(归档解档， 利用runtime遍历模型对象的所有属性)
	*字典 -> 模型， (利用runtime遍历模型所有的属性，根据属性名从字典中取出对应的值，设置到模型的属性上)
	*KVO(动态产生一个类)
	*用于封装框架
3.	相关函数
	*objc_msgSend	消息机制
	*class_copyMethodList	遍历类的所有方法
	*class)copyIvarList		遍历某个类的所有成员变量
4.	必备常识
	*Ivar : 成员变量
	*Method : 成员方法
	
***
	
#### KVC

```
NSArray * getPropertyNameList(id object)  
{  
    unsigned int propertyCount = 0;  
    objc_property_t * properties = class_copyPropertyList([object class], &propertyCount);  
    NSMutableArray * propertyNames = [NSMutableArray array];  
    for (unsigned int i = 0; i < propertyCount; ++i) {  
        objc_property_t property = properties[i];  
        const charchar * name = property_getName(property);  
        [propertyNames addObject:[NSString stringWithUTF8String:name]];  
    }  
    return propertyNames;  
} 

```

```

+（Result*）resultWithDict：(NSDictory*)dict{  
 Result* r = [[Result alloc] init];  
 NSArray* propertyArray = getPropertyNameList(result);  
 for (NSString* key in propertyArray) {  
     @try{  
         if([key isEqual:@"items"]){  
             [result setValue:[Item itemsWitdhArray:dict[key]] forKey:key];  
         }else{  
             [result setValue:dict[key] forKey:key];  
         }  
     }@catch (NSException *exception) {  
         NSLog(@"except:%@:%@",key,dict[key]);  
     }  
 }  
  
 return result;<span style="font-family:Arial,Helvetica,sans-serif">}</span> 

```	


---

**20160825更新**		
Objective-C有两种版本: modern, legacy.		
两者差别：In the legacy runtime, if you change the layout of instance variables in a class, you must recompile classes that inherit from it.	
In the modern runtime, if you change the layout of instance variables in a class, you do not have to recompile classes that inherit from it.	
此外，modern 自动合成实例变量。	

## Messaging
*消息表达式如何转成 objc_msgSend； 
*如何根据方法名引用方法；
*解释如何利用 objc_msgSend；
*并且如果需要，可以实现规避动态绑定。	

只有在运行时，消息才会绑定方法的实现	
[reciever message] -> objc_msgSend(receiver, selector)	
消息传递的关键依赖类和对象的结构体，每个类结构体包含两个基本要素：

*指向父类的指针；
*类的调度表。这个表包含一些实体，实体关联方法的选择器和类指定的这些方法的地址。

当一个对象创建的时候，其内存也会创建。还有实例变量也会初始化。所有这些变量中，首先是指向父类结构体的指针，这个指针叫做**isa**，使这个对象访问到他的类。		
消息发送就是在运行时绑定方法实现的。	
消息查找，先是缓存，再是当前类方法调度表，接着父类直到 NSObject。	
### Using Hidden Arguments
objc_msgSned 找到方法实现的时候，就传递参数过去，另外还有两个隐藏参数:

*接收对象；
*方法的选择器

### Getting a Method Address
唯一的方法规避动态绑定：获取方法的地址，将其当作一个函数一样直接调用。这种用法在一些少有的情况是合适的，一个方法要接连使用很多次，你想避免执行方法时，过度地消息发送。	
NSObject 类有个方法 'methodForSelector:' ，你可以向程序请求实现了这个方法的指针，然后使用这个指针调用这个程序。 'methodForSelector:' 返回的指针必须小心确定其函数类型。返回值和参数都必须包含。	
使用例子：

```
void(* setter)(id, SEL, Bool);
int i;

setter = (void(*)(id, SEL, Bool))[NSObject methodForSelector:@selector(setFill:)];
for (i = 0; i < 1000; i++)
	setter(targetList[i], @selector(setFill:), YES);
```	
这样使用避免动态绑定节省发送消息的时间。但是要在大量的消息发送情况下使用。	
## Dynamic Method Resolution
这个章节描述如何动态添加方法的实现。	
### Dynamic Method Resolution
### Dynamic Loading

## Message Forwarding
将一个消息发送给一个无法处理的对象是一个错误。然而，在报错前，runtime 系统给了消息接受者第二个机会去处理这个消息。		
### Forwarding
报错前，给消息接受者再发送 'forwardInvocation:' 消息，有一个唯一的参数：NSInvocation 对象。这个对象封装了原始消息以及传递过来的参数。	

```
-(NSMethodSignature*)methodSignatureForSelector:(SEL)selector
{
    NSMethodSignature *signature = [super methodSignatureForSelector:selector];
    if (! signature) {
        //生成方法签名
        signature = [_animal methodSignatureForSelector:selector];
    }
    return signature;
}


- (void)forwardInvocation:(NSIvocation *)anInvocation {
	if ([someOtherObject responseToSelector:[anInvocation selector]]) {
		[anInvocation invokeWithTarget:someOtherObject];
	} else {
		[super forwardInvocation:anInvocation];
	}
}
```
这个被传递消息的返回值还是被返回到**原始的发送者**(事情让别人干了，好处自己拿)。所有类型的返回者都可以被传递给发送者。	
'forwardInvocation:' 可以被当作未识别消息的分发中心，分发到不同的接受者。这个消息的可塑造性比较强，只看程序怎么实现。
### Forwarding And Mutiple Inheritance
forwarding 可以达到多继承的效果。多继承是联合不同的功能到单个对象中；Forwarding 是将不同的责任赋予不同的对象。
### Surrogate
proxy 是‘远程通信’中讨论的代理。proxy 负责管理要传递给远程对象的消息的详情，取保连接正常，然后不会做更多事情；它不会定义远程对象的功能，而是给出一个本地地址，远程对象可以在其他应用通过这个地址获取消息。	
某些对象要操作大量的数据（创建复杂的图片或者从磁盘读取数据）。创建这个对象是一个耗时的操作，所以更倾向懒加载（必须使用的时候或者系统空闲的时候）。但此时需要一个占位的对象提供给其他地方使用。	
这种情况下，就可以创建一个轻量级的对象而不是成熟的对象，处理一个事务，要真正处理事务的时候，使用 'forwardInvocation:' ，此时要确保目标对象已经存在，否则创建。消息都是由代理传递过来。
### Forwarding And Inheritance
respondsToSelector:, isKindOfClass:, instancesRespondToSelector:不同于继承，需要手动实现这些方法。	
## Declared Properties


'resolveInstanceMethod:' ‘forwardInvocation:’ 区别 	
前者是一个提供动态实现的机会，如果这里返回 NO ，就会调后者，进行转发机制。
