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

#### 基本使用

1. 通过jps命令查看运行程序的pid
2. 执行 ./profiler.sh start pid开启性能分析
3. 执行 ./profiler.sh stop pid结束性能分析并打印结果

常用命令参数：
- -d 设定持续时间（duration time） 如：./profiler.sh -d 30 8983
- -f dump结果为火焰图并保存到一个SVG文件 如：./profiler.sh -d 30 -f /tmp/flamegraph.svg 8983

默认的采样周期是10ms

#### 与程序一同启动
当需要在程序运行时同步分析，可以在运行时将async-profiler参数附加到命令中

```
$ java -agentpath:/usr/local/async-profiler/build/libasyncProfiler.so=start,file=profiler.svg Test
```
运行Test的过程中会进行分析，并生成火焰图保存到profiler.svg中

## profiler选项

- **start** 开始profiling
- **stop** 停止profiling
- **resume** 开始profiling或者恢复之前停止的profiling会话，参数不会记录，要重新设置
- **check** 检查特定的profiling事件是否可用
- **status** 打印当前的profiling状态，是否在profiling状态并且执行了多久
- **list** 展示可用的profiling事件，需要PID，在不用的虚拟机版本中支持的事件不同
- **-d N** profiling持续时间，以秒为单位，达到时间自动停止profiling
- **-e event** profiling事件，包含cpu，alloc，lock，cache-misses等，可以搭配list查看支持的事件
- **-i N** profiling间隔设置，默认单位为纳秒10000000（10ms），可以在N后加s,ms,us设置其他单位
- **-j N** 设置profiling的栈深度，超过默认2048的值会被忽略
- **-o fmt** 明确在profiling结束时dump的信息
fmt可以是：
    - **summary** dump基本的profiling统计
    - **traces[=N]** dump调用轨迹