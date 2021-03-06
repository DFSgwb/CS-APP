# <center> 计算机系统漫游
### 1.1 信息就是位+上下文
字节：由八个连续的0,1构成的比特(位)序列

只由ASCII字符构成的文件称为文本文件。所有其他文件都被称为二进制文件。

### 1.2程序被其他程序翻译成不同的格式
高级语言的每一条语句都需要被其他程序转化为一系列的低级机器语言指令，然后这些指令按照一种称为可执行目标程序的格式打好包,并以二进制磁盘文件的形式存放起来。目标文件也称为可执行目标文件。
在Unix系统中，源文件到目标文件的转化是由编译器驱动程序完成的，即：
> linux> gcc -o test test.c

这个过程分为四个阶段(以c语言为例)：

1.预处理阶段：预处理器根据以#开头的命令修改原始c程序,生成一个
.i作为文件扩展名的新文件。

2.编译阶段:编译器(ccl)将文本文件.i转化为.s的文本文件，也就是一个汇编程序

3.汇编阶段：汇编器(as)将.s文件翻译为机器语言指令,这些指令打包为可重定位目标程序$(relocatable\ \ object\ \ program)$的格式,得到.o的二进制文件

4.链接阶段：使用链接器(ld)将各各分开的.o文件合并到一个文件中，得到最后的可执行文件

### 1.3系统硬件
#### <center> 系统硬件组成
<div align="center"><img src="..\image\一个典型系统的硬件组成.PNG"></img></div>
总线：贯穿整个系统的一组电子管道被称为总线，携带信息字节并负责在各个部件间传递

I/O设备：系统和外部世界的联系通道

主存：一个临时存储设备,在处理器执行程序时,用来存放程序和程序处理的数据。从物理上来说,主存是一组动态随机存取存储器芯片组成。从逻辑上来说，存储器是一个线性字节数组,每个字节都有其唯一的地址。

处理器:执行存储在主存中指令的引擎,处理器的核心是一个大小为一个字的存储设备(寄存器),称为程序计数器(PC):指向主存中的某条机器语言指令(即含有该指令的地址)


    >加载：从主存复制一个字节或者一个字到寄存器，以覆盖寄存器原来的内容
    >存储：从寄存器复制一个字节或者一个字到主存的某个位置，以覆盖这个位置上原来的内容
    >操作：把两个寄存器的内容复制到ALU，ALU对这两个字做算术运算，并将结果存放到一个寄存器中，以覆盖寄存器中原来的内容
    >跳转：从指令本身中抽取一个字，并将这个字复制到程序计数器（PC）中，以覆盖PC中原来的值

### <center>存储设备的层式结构</center>
<div align="center"><img src="..\image\存储器层次结构.PNG"></img></div>

### 操作系统
操作系统的两个基本功能：

    > 防止硬件被失控的应用程序滥用
    > 向应用程序提供简单一致的机制来控制复杂而又简单大而不同的低级硬件设备
进程：操作系统对一个正在运行的程序的一种抽象，进程和进程之间的转换由OS内核管理的。

并发运行:一个进程的指令和另一个进程的指令是交错执行

上下文:OS中保持跟踪进程运行所需的所有状态信息的状态

线程:OS中能够运行运算调度的最小单位,指的是进程中一个单一顺序的控制流

### Amdahl定律

假设系统执行某应用程序需要时间为$T_old$,假设系统部分所需执行时间与该时间的比例为$\alpha$,而该部分性能提升比例为$k$。即该部分初始所需时间为$\alpha T_{old}$,现在所需时间为$(\alpha T_{old})/k$,因此总的执行时间应为
$$\Large T_{new}=(1-\alpha)T_{old}+(\alpha T_{old})/k=T_{old}[(1-\alpha)-\alpha/k]$$
因此计算加速比$S = T_{old}/T_{new}$为：
$$\Large S = \frac{1}{(1-\alpha)+\alpha/k}$$


### 并发与并行

并发:指一个同时具有多个活动的系统，线程级并发和指令级并发两种

并行:使用并发来使得一个系统运行得更快