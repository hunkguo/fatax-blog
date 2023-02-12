---
title: C语言日期处理
date: 2022/11/7
updated: 
tags:
- C
categories: 人到中年学C语言
---
需求很简单，取当前日期，算出10天前的日期，查询需要提交时间段。首先考虑用时间戳，自以为最简单，没想到无比坑。
<!-- more -->
以下代码的问题是，转出时间均为10天前。
```
    // 取当时时间
    time_t now = time(0);
    // 转换为本地时间struct tm
	tm *e_lt = localtime(&now);

    
	time_t s_tm = time(0);
	// 减去10天
	s_tm -=60*60*24*10;
	tm *s_lt = localtime(&s_tm);
```
后经请教，原来time_t是全局变量，使用指针后，一经修改全都变了。
相当郁闷，在其它语言中的日期处理相当简单，在C中如此麻烦，折腾了好久，才搞明白，在早期的C语言中根本没有日期时间类型的，历史问题，好在新版本中不断完善增加。

最终使用chrono库来解决时间问题，完美。
```
    std::chrono::system_clock::time_point end = std::chrono::system_clock::now();
    std::chrono::system_clock::time_point start = end - std::chrono::hours(24*10);
    time_t tmt_start =  std::chrono::system_clock::to_time_t ( start );
    time_t tmt_end =  std::chrono::system_clock::to_time_t ( end);

    tm tm_start = *localtime(&tmt_start);
    tm tm_end = *localtime(&tmt_end);
```
自我总结下，虽然过程曲折，但增加了对C语言的熟悉，比看直白的入门教程要有效的多。
