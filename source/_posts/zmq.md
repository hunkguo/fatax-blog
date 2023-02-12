---
title: ZMQ
date: 2022/11/9
updated: 
tags:
- C
- ZMQ
categories: 人到中年学C语言
---

# 安装libzmq
```
echo 'deb http://download.opensuse.org/repositories/network:/messaging:/zeromq:/release-stable/Debian_10/ /' | sudo tee /etc/apt/sources.list.d/network:messaging:zeromq:release-stable.list
curl -fsSL https://download.opensuse.org/repositories/network:messaging:zeromq:release-stable/Debian_10/Release.key | gpg --dearmor | sudo tee /etc/apt/trusted.gpg.d/network_messaging_zeromq_release-stable.gpg > /dev/null
sudo apt update
sudo apt install libzmq3-dev
```

# 下载cppzmq
```
wget https://github.com/zeromq/cppzmq/archive/refs/tags/v4.8.1.tar.gz
```
# 解压并安装
```
mkdir build
cd build
cmake ..
sudo make -j4 install
```

# 编译时在CMakeLists.txt加入头文件和库文件。
```
#find cppzmq wrapper, installed by make of cppzmq
find_package(cppzmq)
target_link_libraries(*Your Project Name* cppzmq)
```




