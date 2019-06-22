---
title: auto类型
date: 2019-06-23 00:04:49
tags: [auto, c11]
categories: c++11特性篇
comments: true
---
## 定义
啥是auto类型?
回答这个问题前，我们先看个例子
```c++
for (std::vector<std::string>::iterator it = myvector.begin(); it != myvector.end(); ++it)
这个例子可以优化为:
for (auto it = myvector.begin(); it != myvector.end(); ++it)
```
so，auto类型是能够根据等号右边表达式自动推导出左边变量的类型的修饰符

## 使用方法
auto类型其作用显而易见:
{% blockquote %}
1. 自动推导类型
2. 简化代码
{% endblockquote %}

使用方法举例如下：
```c++
auto a = 1.0;  				// auto解释为double类型
auto it = myvector.begin(); // auto解释为变量myvector的类型的迭代器
```
{% blockquote %}
3. auto还有一个重要作用是使用模板技术时，如果某个变量的类型依赖于模板参数，使用auto自动推导
{% endblockquote %}
```c++
template<class T, class U>
auto add(T t, U u) {
    auto s = t + u;
    return s;
}
```

## 注意事项
使用上应注意：
1. 必须有初始值
```c++
auto a;					// 错误：无法推导类型
```

1. 不能用于函数参数
```c++
void foo (auto a = 1)	// 错误：无法推导类型，即使参数有默认值
```

1. 一条语句中可以声明多个变量, 但同时只能有一个基本数据类型
```c++
auto a = 1, b = 1.0f, c = &a; // 错误: 不支持多种类型
auto x = 1, *y = &x, **z = &y; // OK: auto解释为int
```

1. 在遇到有引用和const修饰时，会把情况变得很复杂，逻辑不明朗，建议不使用或小心使用
```c++
const int a = 0;
const int& b = a;
auto c = b; 	// c是int类型，不是引用，也不具const
auto &d = b;	// auto与&一起，d是const int &类型
```
