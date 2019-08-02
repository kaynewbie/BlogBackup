---
title: runtime-class-object
tags:
- objective-c
- runtime
- ios
- object
---

http://southpeak.github.io/2014/10/25/objective-c-runtime-1/

类和对象的结构体：
```c
typedef objc_class *Class;

struct objc_class {
    Class isa;

    Class super_class;
    struct objc_ivar_list *ivars;
    struct objc_method_list **methodLists;
    struct objc_cache *cache;
    struct objc_protocol_list *protocols;
};

struct objc_object {
    Class isa;
};
typedef struct objc_object *id;
```

实例变量结构体：
```c
struct objc_ivar {
    char *ivar_name;
    char *ivar_type;
    int ivar_offset;
}

struct objc_ivar_list {
    int ivar_count;
    struct objc_ivar ivar_list[1];
};
```

类内部方法缓存的结构体：
```c
struct objc_cache {
    unsigned int mask;
    unsigned int occupied;
    Method buckets[1];
};
```

方法结构体：
```C
typedef struct objc_selector *SEL;
typedef id (*IMP)(id, SEL, ...);

struct objc_method {
    SEL method_name;
    char *method_types;
    IMP method_imp;
};
```

## 类相关操作
* 获取类名
* 获取父类
* 判断是否元类
* 实例变量大小
* 实例变量及属性
  * 实例变量操作
  * 属性操作
* 方法
类实例变量大小是否确定？如果添加方法会影响内存大小吗？
* 协议
* 版本
* 其他

### 例子
### 动态创建类
内存管理??

## 实例操作
* 针对整个对象进行操作的函数
* 针对对象实例变量的操作
* 针对对象所属类的操作

## 获取类的定义