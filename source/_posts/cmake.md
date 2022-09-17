---
title:cmake升级到最新版本
date: 2022-9-17
tags:
	- C
	- cmake
categories: 人到中年学C语言
---
编译cppzmq，总是报错，Unknown CMake command "FetchContent_MakeAvailable"。
始终没答案，偶然搜索到说cmake3.14才支持FetchContent_MakeAvailable，而debian 10的是3.13，立马升级，顺利搞定。
<!-- more -->
# 卸载安装的cmake
```
sudo apt remove cmake
```
# 下载最新版cmake
```
wget https://github.com/Kitware/CMake/releases/download/v3.24.2/cmake-3.24.2.tar.gz
```

# 如果现有系统无cmake
```
./bootstrap
```
# 如果现有系统有cmake（未测试）
```
cmake -DCMAKE_INSTALL_PREFIX=/usr .
```
# 编译
```
make
```
# 编译安装
```
sudo make install
```
搞定