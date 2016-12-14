# Archive

存档提供了一种将对象和值转变成独立结构的字节流，这个字节流保存了关于对象和值的标识。	
支持的数据类型：对象，纯量，数组，结构体，字符串。不支持一些跨平台的数据类型，比如：union, void *, 函数指针, 长链表的指针。	
存档会一同保存对象的类型信息，所以解档之后的数据会和存档之前的一样。解档异常情况可参照这里: [异常情况](xcdoc://?url=developer.apple.com/library/ios/documentation/Cocoa/Conceptual/Archiving/Articles/codingobjects.html#//apple_ref/doc/uid/20000948-97072)。	  
<!-- more -->

## Coders
对象要通过**编码对象**写入或读取存档。编码对象是 NSCoder(抽象类) 之类的实例。 NSCoder 声明一个广泛的接口，用来保存信息到对象中并且放到其他适合写入到文件中的格式，在程序或者不同网络之间传递，或者执行其他数据类型的交换。也有翻转数据类型的接口。子类实现合适的接口支持特殊的存档格式。	
编码对象通过适当的方法编解码。存档：发送 encodeWithCoder: 给对象，解档：发送 initWithCoder:。只有遵循了 NSCoding 协议，才能存档。编码时，编码对象纪录对象的类的标识或者 OC 值的类型的标识以及在层级结构中的位置。	
为了解决冗余和约束的问题，引入根对象和条件对象。	

### Root Object
两个对象可能互相引用，造成循环引用。如果编码对象盲目编码，可能会无限循环。单个对象也可能被多个对象引用，编码对象必须区别并处理多个引用或者循环引用，保证编解码正常。	
解决以上问题，引入根对象。根对象是对象图中的起点。调用编码方法，传入第一个对象开始编码。在这个调用环境中的每个对象都可以被追踪。如果要多次编码同一个对象，只会编码引用而不会重新对该对象编码。	
NSCoder 不会实现对根对象的支持；NSCoder 的 encodeRootObject: 实现，通过调用 encodeObject: 编码对象。他的子类有责任追踪多个引用的对象，这样来保存任何对象图的结构题。	
### Conditional Object
有些对象图不适合完全编码。比如某个视图引用了非常多对象（window, target），可能牵扯到整个应用。有些父视图就不需要存档。如果父视图也存档的话，就要对父视图引用。	
条件对象可以解决这个问题。一个条件对象应该被编码，当且仅当，在其他地方被无条件的编码。条件对象通过 encodeConditionalObject:forKey: 编码。如果所有请求编码对象都是通过这些条件方法，那这个对象不能被编码，并且引用他的解码是空。如果这个对象在其他地方被编码了，所有条件引用解码到单独的编码对象。	
NSCoder 不实现对条件对象的支持；NSCoder 的 encodeConditionalObject:forKey: 实现，通过调用 encodeObject:forKey: 编码对象。子类有责任追踪条件对象，并且除非对象需要，否则不对其编码。	

## Keyed Archives
Keyed Archives 是通过 NSKeyedArchiver 对象创建，NSKeyedUnarchiver 解码。Keyed Archives 在编码值方面不同于有序的存档，他是给定名字或者键。解码存档时，通过名字请求值，允许值按任意顺序或者无序请求。这种自由度给类更灵活地向前兼容或向后兼容。	

### Naming Values
对象编码到文档中的值可以单独地用任意字符串命名。文档时分层级的，每个对象编码的值都定义了单独的命名空间，和对象的实例变量类似。因此，当前对象编码的作用域内是键是唯一的。但是不同的对象键不会冲突，即使是同一个类。单个的对象中，子类的键会和父类的键冲突。	
对于一些公共的可以子类化的类，名字要添加一些前缀来避免以后子类可能用到。合理的前缀是类的全名。	
避免使用'$'。	
子类也要一定程度上当心前缀的使用，避免和父类冲突。

### Return Values For Missing Keys
解码期间，如果一个键的值不存在，解档对象就会根据调用方法的返回值返回默认值（nil for objects, NO for booleans, 0.0 for reals, NSZeroSize for sizes, and so on）。可以用 containsValueForKey: 方法检测是否存在这个键。但不推荐，影响性能，返回值就已经足够了。

### Type Coercions
NSKeyedUnarchiver 支持限制类型强制转换。整形编码，解码后可以是任意整形。浮点类似。编码的值类型相对解码过大，会抛出异常。[NSRangeException](xcdoc://?url=developer.apple.com/library/ios/documentation/Cocoa/Reference/Foundation/Miscellaneous/Foundation_Constants/index.html#//apple_ref/doc/c_ref/NSRangeException)。此外，浮点整形互转会抛异常[NSInvalidUnarchiveOperationException](xcdoc://?url=developer.apple.com/library/ios/documentation/Cocoa/Reference/Foundation/Classes/NSKeyedUnarchiver_Class/index.html#//apple_ref/doc/c_ref/NSInvalidUnarchiveOperationException)。	

### Class Versioning
### Root Objects
### Delegates
NSKeyedArchiver, NSKeyedUnarchiver都有代理。
### Non-Keyed Coding Methods
可以使用没有没有键的编码，但不提倡。

# Creating and Extracting Archives
## Create an Archive
被编码对象要遵循 NSCoding 协议，实现协议方法：

```
- (instancetype)initWithCoder:(NSCoder *)aDecoder {
    if (self = [super init]) {
        _name = [aDecoder decodeObjectForKey:NSStringFromSelector(@selector(name))];
        _age = [aDecoder decodeIntegerForKey:NSStringFromSelector(@selector(age))];
        _gender = [aDecoder decodeObjectForKey:NSStringFromSelector(@selector(gender))];
    }
    return self;
}

- (void)encodeWithCoder:(NSCoder *)aCoder {
    [aCoder encodeObject:_name forKey:NSStringFromSelector(@selector(name))];
    [aCoder encodeInteger:_age forKey:NSStringFromSelector(@selector(age))];
    [aCoder encodeObject:_gender forKey:NSStringFromSelector(@selector(gender))];
}
```
archive:	

```
Person* aPerson = [Person new];
    aPerson.name = @"Kai";
    aPerson.age = 24;
    aPerson.gender = @"male";
    
    NSMutableData* data = [[NSMutableData alloc] init];
    NSKeyedArchiver* archiver = [[NSKeyedArchiver alloc] initForWritingWithMutableData:data];
    [archiver encodeObject:aPerson forKey:personKey];
    [archiver finishEncoding];
    
    NSString* path = [self pathForArchive];
    BOOL result = [data writeToFile:path atomically:YES];
```
unarchive:

```
NSData* data = [NSData dataWithContentsOfFile:path];
    
    NSKeyedUnarchiver* unarchiver = [[NSKeyedUnarchiver alloc] initForReadingWithData:data];
    id obj = [unarchiver decodeObjectForKey:personKey];
    [unarchiver finishDecoding];
```
# Encoding and Decoding Objects
## Encoding an Object
如果一个对象的父类也遵循了 NSCoding 协议，需要先调用父类的 encodeWithCoder: 。

## Decoding anObject
如果一个对象的父类也遵循了 NSCoding 协议，需要先调用父类的 initWithCoder: 。

### Performance Considerations
编码越少，解码就越少，读写速度就会更加快。只写和类相关的项目。	
不需要的项不要将其写出。	
尽量不要使用 containsValueForKey: ，除非要区分空值的默认值和真实值相同的情况。	
加速解码比加速编码更有意义。	
避免使用'$'。

## Making Substitutions During Coding

# Serializing Property List
NSPropertyListSerialization