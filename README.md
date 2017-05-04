# rtems_book
# rtems internal and development
## 前言
07年，我还在倒腾rtems.net网站的时候陈瑜教授对这个操作系统也挺感兴趣，有意在清华开设操作系统实作课程，并以RTEMS为蓝本授课。我个人认为相对Linux，rtems对操作系统的初学者无疑更加适合。尤其是对于实时调度，与我接触的商用级别vxWorks, lynxOS并无明显差距，对于ucOSII和ThreadX/freeRTOS则有明显优势。我们在邮件组里讨论了一下，分工完成了此书。

本来计划交由清华出版社付梓，可惜后来一直没有实现。 考虑到我们开始对开源的初衷，我想把写好的部分放在Github上是一个更好的选择。现在Rtems已经4.11了，原书是针对4.8所写。但是其中大部分内容任对读者了解和使用Rtems会有很大帮助。

文章中错漏的地方，欢迎提交issue。如果有热情，也欢迎继续为本书补充内容， 谢谢！如果Fork，请附上完整的README.md谢谢

## 目录
### 第一章 RTEMS硬实时操作系统简介
### 第二章 基本开发和调试过程
  本章涉及的主要内容包括RTEMS源码的获取，源码树结构介绍，开发环境的建立以及如何运行RTEMS的测试用例、开发应用程序和调试应用程序
### 第三章 总体结构和系统构成
  RTEMS的设计目标、总体设计思路、总体架构进行分析；并进一步对RTEMS的底层系统支持机制进行阐述；接下来对构成RTEMS主要功能的核心组件进行描述，并说明它们之间的交互关系；最后对RTEMS的核心代码结构进行描述。这一章内容较多，开始结合代码的干货和实际分析也都很多。着重介绍了包括信号量，互斥的基础， RTEMS对象结构体设计等内容
### 第四章 初始化过程
  在操作系统课本中，很少涉及到操作系统启动要做的事情，以及操作系统是如何开始正常运行等问题。导致读者虽然知道进程/线程管理、内存管理、同步互斥等抽象出来的操作系统原理，但对于让操作系统和上述机制开始正常工作的启动和初始化过程不太清楚。就好比虽然吃到了免淘洗的精制白米饭，感到饭也很好吃，但在把谷子变成糙米再变成精米的过程中，很多有营养的成分已经丢失了。下面各节将讲解计算机硬件的启动、引导加载程序、BIOS、加载RTEMS操作系统的OS boot loader和RTEMS操作系统的具体初始化启动过程。
### 第五章 线程管理与调度
  RTEMS是一个以线程（也称任务）为基本调度单位的实时操作系统。调度算法是基于优先级的抢占式线程调度，支持256个线程优先级。结合任务控制块，优先位图，等待队列等关键结构体分析了RTEMS线程实时调度的实现。 最后结合测试用例，讲解了任务管理API的使用。
### 第六章 中断处理
  本章主要讲解RTEMS中断处理的设计与实现，涉及中断和异常的介绍、中断的建立过程、中断的处理过程、中断的机制、中断上下文、嵌套中断等
### 第七章 时间服务
  精确的时间管理对于商业级别的操作系统非常重要。本章将对在核心层和系统服务层的相关组件为提供RTEMS时钟服务而进行的设计与实现进行分析，对timer manager组件提供的上层时间服务接口进行描述。从而让读者在设计实时应用是能够更好地实用时钟服务。
### 第八章 同步互斥与通信机制
  在RTEMS中，内核提供了信号量（Semaphore）、栅栏（Barrier）自旋锁、（SpinLock）、读写锁（RWLock）等同步互斥机制以及消息队列（Message Queue）、事件（Event）等通信机制。这些机制的实现主要在系统服务层，并建立在核心层的基础之上，所以本章每部分机制实现的分析包括核必层和系统服务层两部分。
### 第九章 内存管理
  内存管理机制是实时操作系统的重要组成部分。从实时性的角度出发，要求内存分配过程的时间要尽可能的确定和快速。文中关于内存保护的说法有些旧。但是总体而言，为了实时性，RTEMS任然是扁平结构的内存管理。14年开始有了MMU
### 第十章 文件系统
  主要分析了RTEMS支持的IMFS和FAT，目前YAFFS, JFFS2也都有支持。但是这些系统是GPL的，所以不在源代码树里面
### 第十一章 I/O系统
  在计算机系统中，有大量的输入输出设备，其种类繁多，差异大。而且随着技术的发展，新设备也不断地出现。因此，如何管理好这些设备，使资源得以合理的利用，是操作系统的一个主要功能，此功能由操作系统的主要组成部分—I/O系统完成。I/O系统要能使这些设备能够运转起来，包括给它们发送控制命令、捕获中断、错误处理等；同时它还需要在这些设备与系统的其他部分之间，提供一个简单、易用的接口，并尽可能地使这个接口适用于所有的设备，即实现与设备的无关性。
### 第十二章 裁减定制与移植
  RTEMS有很好的可移植性与可剪裁性，可移植主要是指能将RTEMS移植到新的硬件上，而剪裁与定制指的是根据硬件以及应用程序的需要，对RTEMS库进行配置，使最后生成的可执行代码满足用户的需要。