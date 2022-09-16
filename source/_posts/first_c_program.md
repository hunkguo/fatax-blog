---
title: 第一个C语言程序
date: 2022-9-16
tags:
	- C
categories: 人到中年学C语言
---
上学时，C语言是入门课程，但毕业后，从没用过。券商只有C语言SDK，咬牙看起来，谁成想，体验还不错，虽然有些坑，慢慢在此记录。
<!-- more -->
项目结构
├── build
├── CMakeLists.txt
├── include
└── src
    └── hello.cpp
主程序超级简单，而且完全是课本上的味道，体验一下。
hello.cpp
```
#include <iostream>
#include <chrono>
int main()
{
    // char name[50];
    // std::string msg="hello world!";
    // std::cout << "请输入您的名称： ";
    // std::cin >> name;
    // std::cout << "您的名称是： " << msg << name << std::endl;

    return 0;
}


```
CMakeLists.txt
这里感觉有些小成就感，cmake用了不少，自己写还是头一次。
cmake .. && make运行以后，程序就能执行了，好新鲜。成就感+1
```

#1.cmake verson，指定cmake版本
cmake_minimum_required(VERSION 3.2)

#2.project name，指定项目的名称，一般和项目的文件夹名称对应
PROJECT(hello)

#3.head file path，头文件目录
INCLUDE_DIRECTORIES(
include
)

#4.source directory，源文件目录
AUX_SOURCE_DIRECTORY(src DIR_SRCS)

#5.set environment variable，设置环境变量，编译用到的源文件全部都要放到这里，否则编译能够通过，但是执行的时候会出现各种问题，比如"symbol lookup error xxxxx , undefined symbol"
SET(TEST_MATH
${DIR_SRCS}
)

#6.add executable file，添加要编译的可执行文件
ADD_EXECUTABLE(${PROJECT_NAME} ${TEST_MATH})

#7.add link library，添加可执行文件所需要的库，比如我们用到了libm.so（命名规则：lib+name+.so），就添加该库的名称
TARGET_LINK_LIBRARIES(${PROJECT_NAME} m)
```
