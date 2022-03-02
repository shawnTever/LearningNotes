# 线程、线程池、线程池监控

- [线程、线程池、线程池监控](#线程线程池线程池监控)
  - [线程](#线程)
    - [进程、线程、主线程](#进程线程主线程)
    - [串行、并发、并行](#串行并发并行)
    - [如何进行通讯](#如何进行通讯)
  - [并发三大特性](#并发三大特性)
  - [线程数多少合适](#线程数多少合适)
  - [6种线程状态](#6种线程状态)
    - [submit()和execute之间的区别](#submit和execute之间的区别)
    - [返回值Future](#返回值future)
  - [线程打断interrupt](#线程打断interrupt)
  - [强引用](#强引用)
  - [currentThread()方法获得当前线程](#currentthread方法获得当前线程)
  - [getname()方法获得线程名字](#getname方法获得线程名字)
  - [setName()和getName()](#setname和getname)
  - [isAlive()是否处于活动状态](#isalive是否处于活动状态)
  - [sleep(millis)休眠](#sleepmillis休眠)
  - [ThreadLocal()方法](#threadlocal方法)
  - [sleep()、yield()、join()、wait()](#sleepyieldjoinwait)
  - [synchronized和volatile](#synchronized和volatile)
  - [线程池](#线程池)
    - [基本结构](#基本结构)
    - [JDK对线程池支持](#jdk对线程池支持)
    - [Executors提供四种线程池工厂方法](#executors提供四种线程池工厂方法)
    - [线程池监控](#线程池监控)

- [主页](README.md)

## 线程

### 进程、线程、主线程

**程序**：可执行文件

**进程**：正在操作系统中运行的程序，是操作系统进行资源分配与调度的基本单位。

**线程**：进程的一个执行单元。一个线程就是进程中单一顺序的控制流，进程执行的一个分支。在操作系统中以进程为单位分配资源，如虚拟存储空间、文件描述符。每个线程都有各自的线程栈、自己的寄存器环境、自己的线程本地存储。

**主线程**：Java启动时会创建一个主线程，该主线程负责执行main方法。

### 串行、并发、并行

**串行**：先做任务A，完成后再做任务B，完成后再做任务C

**并发**：先做任务A，准备5分钟之后开始任务B，准备2分钟之后开始任务C，等待10分钟之后任务C结束（可以提高事物处理效率）

**并行**：三个任务同时开始

从硬件角度来说，如果是单核cpu一次只能执行一个线程的情况下，处理器可以使用时间轮转技术

### 如何进行通讯

可通过共享内存或基于网络进行通讯

共享内存：java中wait(), notify()

网络：通过网络连接将通信数据发送给对方

## 并发三大特性

**原子性**：是指在一个操作中**cpu不可以在中途暂停**然后再调度，即不被中断，要不全部执行完成，要不都不执行

**可见性**：当多个线程访问同一个变量的时候，一个线程修改了这个变量值，**其他线程能够立即看到修改的值**。

**有序性**：虚拟机在进行代码编译时，对于那些改变顺序之后不会对结果有影响的代码，虚拟机**不一定会按照我们写的代码来执行**，有可能讲他们重排序

## 线程数多少合适

由于线程转换需要资源，所以并非线程越多越好，理论上线程数量 = CPU 核数（逻辑）就可以了，但是实际上，数量一般会设置为 CPU 核数（逻辑）+ 1。

考虑到线程等待时间与CPU利用率，参考《Java并发编程实战》N（threads）=N（CPU）\*U（CPU）\*（1 + W/C）

N（CPU）处理器核数

U（CPU）CPU利用率

W等待时间，C计算时间


## 6种线程状态

new：线程刚刚创建，还没有启动

runnable：可运行状态，由线程调度器可以安排执行

waiting：等待被唤醒

timed waiting：隔一段时间后自动唤醒

blocked：被阻塞，等待解锁，只有synchronized状态下（经过操作系统调度）线程产生blocked状态，lock下线程产生waiting状态

terminated：线程结束

park：LockSupport类中的方法

### submit()和execute之间的区别

submit()方法，可以提供Future < T > 类型的返回值。

executor()方法，无返回值.

### 返回值Future

Future表示一个可能还没有完成的异步任务的结果，线程运行结束之后，将返回值给Future

```java
        ExecutorService service = Executors.newCachedThreadPool();
//        Future表示一个可能还没有完成的异步任务的结果，线程运行结束之后，将返回值给Future
        Future<String> f = service.submit(new createByCallable());
//        get()为阻塞类型，线程结束之后拿到返回值之后继续运行程序
        String s = f.get();
```

## 线程打断interrupt

interrupt()：打断某个线程（设置标志位）

isInterrupted()：查询某线程是否被打断过（查询标志位）

static interrupted()：查询当前线程是否被打断过，并重置打断标志

## 强引用

平时我们编程的时候例如：Object object=new Object（）；那object就是一个强引用了。如果一个对象具有强引用，那就类似于必不可少的生活用品，垃圾回收器绝不会回收它。当内存空 间不足，Java虚拟机宁愿抛出OutOfMemoryError错误，使程序异常终止，也不会靠随意回收具有强引用的对象来解决内存不足问题。

## currentThread()方法获得当前线程

currentThread()方法是静态方法，Thread.currentThread()方法可获得当前线程，返回值是在代码实际运行时候的线程对象。

## getname()方法获得线程名字

getname()方法获得当前线程名字。

## setName()和getName()

thread.setName(线程名称) 设置线程名称

thread.getName()返回线程名称

## isAlive()是否处于活动状态

thread.isAlive()判断当前线程是否处于活动状态

## sleep(millis)休眠

Thread.sleep(millis);让当前线程休眠制定毫秒数。

## ThreadLocal()方法

ThreadLocal的作用主要是做数据隔离，填充的数据只属于当前线程，变量的数据对别的线程而言是相对隔离的。

## sleep()、yield()、join()、wait()

**sleep()**：让**其他线程走，自己进行休眠，但是自己却不会释放对象锁**，也就是说，如果有同步锁的时候，其他线程不能访问共享数据。sleep()可以使低优先级的线程得到执行的机会，当然也可以让同优先级、高优先级的 线程有执行的机会。

**yield()**：执行后直接**进入就绪状态**，同样不会释放自身锁的标识，区别在于它是**没有参数**的，即yield()方 法只是使**当前线程重新回到可执行状态**，因此下一次线程调度可能还会让这个线程获取执行权继续执行。yield()方法只能使同优先级或者高优先级的线程得到执行机会。

**join()**：当前线程**调用其他线程的join方法**，会阻塞当前线程，直到其他线程执行完毕，才会进入就绪状态。

## synchronized和volatile

通过 synchronized 关键字来实现，所有加上synchronized 和 块语句，在多线程访问的时候， 同一时刻只能有一个线程 能够用

用volatile修饰的变量，线程在每次使用变量的时候，都会读取变量修改后的最后值。

volatile主要用在多个线程感知实例变量被更改了场合，从而使得各个线程获得最新的值。它强制线程每次从主内存中讲到变量，而不是从线程的私有内存中读取变量，从而保证了数据的可见性。

**比较：**

①volatile轻量级，只能修饰变量。synchronized重量级，还可修饰方法

②volatile只能保证数据的可见性，不能用来同步，因为多个线程并发访问volatile修饰的变量不会阻塞。

synchronized不仅保证可见性，而且还保证原子性，因为，只有获得了锁的线程才能进入临界区，从而保证临界区中的所有语句都全部执行。多个线程争抢synchronized锁对象时，会出现阻塞。

## 线程池

**线程池**就是有效使用线程的一种常用方式，线程池内部可以预先创建一定数量的工作线程，客户端代码直接将任务作为一个对象提交给线程池，线程池将这些任务缓存在工作队列中，线程池中的工作线程不断的从队列中取出任务并执行。

### 基本结构

```java
public ThreadPoolExecutor(int corePoolSize,  int maximumPoolSize,  long keepAliveTime,  TimeUnit unit,  BlockingQueue<Runnable> workQueue,  ThreadFactory threadFactory, RejectedExecutionHandler handler)
```

使用线程池的execute方法将Runnable提交到线程池中进行执行。

- 先判断线程池中的核心线程们是否空闲，如果空闲，就把这个新的任务指派给某一个空闲线程去执行。如果没有空闲，并且当前线程池中的核心线程数还小于 corePoolSize，那就再创建一个核心线程。

- 如果线程池的线程数已经达到核心线程数，并且这些线程都繁忙，就把这个新来的任务放到等待队列中去。

- 如果等待队列又满了，那么查看一下当前线程数是否到达maximumPoolSize，如果还未到达，就继续创建线程。如果已经到达了，就交给RejectedExecutionHandler来决定怎么处理这个任务。

### JDK对线程池支持

JDK提供了executor（基本线程池接口）提供executor方法可以向线程池提交任务。

子接口ExecutorService，提供submit(Callable接口)返回值Future，提交runnable任务和Callable任务，shutdown()关闭线程池，其实现类ThreadPoolExecutor实现ExecutorService接口。

子接口ScheduledExecutorService，提供调度方法schedule()可以在指定的事件指定的任务，其实现类ScheduledThreadPoolExecutor。

### Executors提供四种线程池工厂方法

newCachedThreadPool创建一个可缓存线程池，如果线程池长度超过处理需要，可灵活回收空闲线程，若无可回收，则新建线程。

newFixedThreadPool 创建一个定长线程池，可控制线程最大并发数，超出的线程会在队列中等待。

newScheduledThreadPool 创建一个定长线程池，支持定时及周期性任务执行。

newSingleThreadExecutor 创建一个单线程化的线程池，它只会用唯一的工作线程来执行任务，保证所有任务按照指定顺序(FIFO, LIFO, 优先级)执行。

### 线程池监控

线程池使用不当会使服务器资源枯竭，导致异常情况的发生，比如固定线程池的阻塞队列任务数量过多、缓存线程池创建的线程过多导致内存溢出、系统假死等问题。因此我们需要一种简单的监控方案来监控线程池的使用情况，比如完成任务数量、未完成任务数量、线程大小等信息。

| 方法 | 含义 |
| ----------- | ----------- |
| int getActiveCount() | 线程池中正在执行任务的线程数量 |
| long getCompletedTaskCount() | 线程池已完成的任务数量，该值小于等于taskCount |
| int getCorePoolSize() | 线程池的核心线程数量 |
| int getLargestPoolSize() | 线程池曾经创建过的最大线程数量。通过这个数据可以知道线程池是否满过，也就是达到了maximumPoolSize |
| int getMaximumPoolSize() | 线程池的最大线程数量 |
| int getPoolSize() | 线程池当前的线程数量 |
| long getTaskCount() | 线程池已经执行的和未执行的任务总数 |
| BlockingQueue\<Runnable> getQueue() | 返回阻塞队列 |

```java
public ThreadPoolExecutor(int corePoolSize, // 1 

int maximumPoolSize, // 2 

long keepAliveTime, // 3 

TimeUnit unit, // 4

BlockingQueue<Runnable> workQueue, // 5 

ThreadFactory threadFactory, // 6

RejectedExecutionHandler handler ) // 7
```

1. corePoolSize int 核心线程池大小
2. maximumPoolSize int 最大线程池大小
3. keepAliveTime long 线程最大空闲时间
4. unit TimeUnit 时间单位
5. workQueue BlockingQueue\<Runnable> 线程等待队列
6. threadFactory ThreadFactory 线程创建工厂
7. handler RejectedExecutionHandler 拒绝策略
