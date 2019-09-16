---
title: FAQ For ConcurrentHashMap
date: 2019-09-15 15:08:17
---

> 这是Cmap的斜体部分的补充，意图在于不干扰主思路的进行，主体文章详见 {% post_link ConcurrentHashMap ^ConcurrentHashMap %}

Q: Jdk1.7中Cmap的Segment数量是一经创建就不可修改的吗？

A: 是的，这里参照Cmap在1.7中的源码部分：

``` java
  /**
     * 散列映射表的默认初始容量为 16，即初始默认为 16 个桶
     * 在构造函数中没有指定这个参数时，使用本参数
     */
    static final int DEFAULT_INITIAL_CAPACITY= 16;
```

`static` 意味着这个变量的生命周期和类的初始化相同，对等为全局。
`final` 意味着这个变量一经初始化不可修改。

二者结合，等价于一经初始化就不可修改，所以说Cmap在Jdk1.7的情况下并发能力在初始化的时候就是固定好的，扩容也只是增加了不同 `Segment` 内部的HashEntry数量而已。
