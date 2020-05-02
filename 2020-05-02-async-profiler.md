---
title: async-profiler
auther: ahou
layout: post
description: Java 应用性能分析工具
categories: general
---

## async-profiler
**[async-profiler的Github项目地址](https://github.com/jvm-profiling-tools/async-profiler#download)**

**参考文章：[工具介绍](https://www.jianshu.com/p/9364028cca4e)，[实现细节](https://www.jianshu.com/p/19c2f211173b)**

#### 介绍
**参考README.md**
async-profiler是一个对Java应用进行性能分析的工具，通过采样对应用的运行情况进行分析  
基于JVM的接口与JVM进行交互，收集Java堆栈信息和跟踪内存分配

async-profiler可以跟踪的事件：
- CPU周期
- 硬件和软件性能计数器，如缓存未命中，分支未命中，页面错误和上下文切换等
- Java堆中的分配
- 满足的锁定尝试，包括Java对象监视器和Reentrant Locks

#### 使用方式

1. 通过jps命令查看运行程序的pid
2. 执行 ./profiler.sh start pid开启性能分析
3. 执行 ./profiler.sh stop pid结束性能分析并打印结果

常用命令参数：
- -d 设定持续时间（duration time） 如：./profiler.sh -d 30 8983
- -f dump结果为火焰图并保存到一个SVG文件 如：./profiler.sh -d 30 -f /tmp/flamegraph.svg 8983