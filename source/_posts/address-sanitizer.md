---
title: 用 Address Sanitizer 调试内存问题
tags:
  - LLVM
  - address-sanitizer
  - memory-error
  - C/C++
  - buffer-overflow
date: 2019-07-27 23:32:58
---

最近，考虑到自身算法和数据结构基础薄弱，想在平日做些积累，保持对算法的敏感性。于是，开始整上了 "剑指 Offer" 并在 Leetcode 上刷题。

刷题过程中，碰到些题目需要动态开辟内存，如 *[Longest Common Prefix](https://leetcode.com/problems/longest-common-prefix/)* 和 *[Count and Say](https://leetcode.com/problems/count-and-say/)*。于是，在解题过程中，使用了 C 的一些动态[开辟内存函数](https://en.wikipedia.org/wiki/C_dynamic_memory_allocation#Usage_example)，在 Xcode 中编写完成且通过测试用例后，将代码贴到 Leetcode 上，运行报错：
```
AddressSanitizer: heap-buffer-overflow on address 0x6040000000fc at pc 0x00000040196c bp 0x7fffa37d1930 sp 0x7fffa37d1928
```
<!-- more -->

看到错误信息，不了解什么是 **AddressSanitizer**，于是开始查阅资料，作些记录。

另外，因为内存管理在任何开发语言中都是重要知识点，所以作此笔记。

## 什么是 AddressSanitizer

AddressSanitizer(ASan) 是 Google 开源的一个快速发现内存错误的检查器。它能定位以下问题：
* 使用被释放的内存（野指针）
* 堆区缓存溢出
* 栈区缓存溢出
* 全局区缓存溢出
* 在返回后使用
* 作用域外使用
* 初始化顺序问题
* 内存泄露

ASan 由编译期组件和运行时库组成，现已集成到 *LLVM* 中。

## 如何碰到此问题

在解 
*[Longest Common Prefix](https://leetcode.com/problems/longest-common-prefix/)* 过程中，起初算法如下：遍历二维数组首个元素，遍历过程中用当前的字符去匹配二维数组剩下元素对应索引的字符，匹配成功则存到新开辟的内存块中，存之前判断内存块容量是否足够，不足够则扩展内存。
```C
char *longestCommonPrefix(char ** strs, int strsSize){
    int capacity = 5;
    char *pInFirstStr = *strs;
    char *result = malloc(sizeof(char) * capacity);
    int idx = 0;
    
    int i;
    char c;
    bool success;
    while (*(pInFirstStr + idx) != '\0') { // 遍历首元素的字符
        success = true;
        for (i = 0; i < strsSize; i++) { // 用当前字符匹配二维数组剩余元素
            c = *(*(strs + i) + idx);
            if (*(pInFirstStr + idx) != c) {// 匹配失败，则终止，说明已经找到最长公共子字符串
                success = false;
                break;
            }
        }
        if (!success) {
            break;
        }
        if (idx >= capacity) {// 内存扩容
            capacity += 10;
            result = realloc(result, capacity);
        }
        result[idx] = *(pInFirstStr + idx); // 记录公共子字符串
        idx++;
    }
    return result;
}
```

Leetcode 上的[提交记录](https://leetcode.com/submissions/detail/244034342/)。

## 如何解决此问题

首先，考虑到 Xcode 中运行相同测试用例并没有碰到此错误，查阅发现，Xcode 默认并未开启 ASan 选项，于是先打开 ASan：
*在 Xcode 中开启 ASan: Edit Scheme -> Run -> Disgnostics -> Runtime Sanitization*。

接着，跟想象中的一样，运行报了相同的内存错误。反复检查代码，发现，不需要提早开辟内存块，因为最长公共子字符串肯定是包含在数组元素中。

于是，优化代码：
```C
int commonPrefixLength(char *first, int firstL, char *second);

/**
 1. 声明最长共同前缀指针，起始指向第一个字符串
 2. 声明最长共同前缀长度
 3. 遍历
 4. 遍历结束后，从第一个字符串中拷贝出指定长度的字符串
 */
char *longestCommonPrefix(char ** strs, int strsSize){
    if (strsSize <= 0) {
        return "";
    }
    
    char *firstStr; // 第一个字符串
    char *currentS; // 遍历过程中的当前字符串
    int prefixLength; // 遍历过程中的最长公共前缀长度
    
    firstStr = *strs;
    prefixLength = (int)strlen(firstStr);
    
    for (int i = 1; i < strsSize; i++) {
        currentS = strs[i];
        
        prefixLength = commonPrefixLength(firstStr, prefixLength, currentS);
        if (prefixLength == 0) {
            break;
        }
    }
    char *result = malloc((sizeof(char) * prefixLength) + 1);
    memcpy(result, firstStr, prefixLength);
    result[prefixLength] = '\0';
    return result;
}

/**
 获取两个字符串最大前缀长度
 */
int commonPrefixLength(char *first, int firstL, char *second) {
    int commonL = 0;
    while (commonL < firstL && *first != '\0' && first[commonL] == second[commonL]) {
        commonL++;
    }
    return commonL;
}
```
[Leetcode 提交记录](https://leetcode.com/submissions/detail/246388133/)。

上述代码，**将开辟内存空间放在最后且只会根据 `prefixLength` 创建一次，避免了复杂的扩容过程**。

## 小结

如何避免编码过程中出现类似的内存问题：
* 开发时尽量使用 ASan 调试代码
* 在必要的时候再去开辟内存
* 充足的测试用例

## 参考

* [Address Sanitizer Repo](https://github.com/google/sanitizers)
* [Address Sanitizer Wiki](https://github.com/google/sanitizers/wiki/AddressSanitizer)