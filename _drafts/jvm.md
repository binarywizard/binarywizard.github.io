# 深入理解Java虚拟机

1. Java虚拟机运行时数据区
    - 方法区 Method Area
    - 虚拟机栈 VM Stack
    - 本地方法栈 Native Method Stack
    - 堆 Heap
    - 程序计数器 Program Counter Register
        - 字节码解释器工作时是通过改变程序计数器的值来选取下一条需要执行的字节码指令
        - 分支、循环、跳转、异常处理、线程恢复等基础功能都需要依赖程序计数器
        - 每条线程都需要独立的程序计数器
        - 如果线程正在执行的是一个Java方法，这个计数器记录的是正在执行的虚拟机字节码指令地址；如果正在执行的是Native方法，这个计数器值为空（Undefined）
        - 此区域是唯一一个在Java虚拟机规范中没有规定任何OutOfMemoryError情况的区域
