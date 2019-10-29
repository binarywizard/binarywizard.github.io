# 深入理解Java虚拟机

1. Java虚拟机运行时数据区
    - 方法区 Method Area
    - 虚拟机栈 VM Stack
        - Java虚拟机栈也是现成私有的
        - 虚拟机栈描述的是Java方法执行的内存模型：每个方法在执行的同时会创建一个**栈帧**用于存储**局部变量表**、**操作数栈**、**动态链接**、**方法出口**等信息
        - 局部变量表存放了基本数据类型（boolean/byte/char/short/int/float/long/double）、对象引用和returnAddress类型（指向了一条字节码指令的地址）
        - long/double占用2个局部变量空间（Slot），其余数据类型占用1个，所以一个方法需要在帧中分配多大的局部变量空间是完全确定的
        - 如果线程请求的栈深度大于虚拟机所允许的深度，将跑出**StackOverflowError**；如果虚拟机栈可以动态扩展，但扩展时无法申请到足够内存，就会抛出**OutOfMemoryError**
    - 本地方法栈 Native Method Stack
        - 为虚拟机使用的Native方法服务
    - 堆 Heap
    - 程序计数器 Program Counter Register
        - 字节码解释器工作时是通过改变程序计数器的值来选取下一条需要执行的字节码指令
        - 分支、循环、跳转、异常处理、线程恢复等基础功能都需要依赖程序计数器
        - 每条线程都需要独立的程序计数器
        - 如果线程正在执行的是一个Java方法，这个计数器记录的是正在执行的虚拟机字节码指令地址；如果正在执行的是Native方法，这个计数器值为空（Undefined）
        - 此区域是唯一一个在Java虚拟机规范中没有规定任何OutOfMemoryError情况的区域
