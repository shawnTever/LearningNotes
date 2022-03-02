# Operation System and JVM

- [Operation System and JVM](#operation-system-and-jvm)
  - [CPU乱序执行](#cpu乱序执行)
    - [CUP层面如何禁止重排序](#cup层面如何禁止重排序)
    - [JVM层级的4个内存屏障](#jvm层级的4个内存屏障)
    - [as if serial 单线程执行结果不变](#as-if-serial-单线程执行结果不变)

## CPU乱序执行

### CUP层面如何禁止重排序

内存屏障，对某部分内存做操作时前后添加的屏障，屏障前后的操作不可以乱序执行。

### JVM层级的4个内存屏障

JSR内存屏障：

LoadLoad：对于这样的语句Load1;LoadLoad;Load2，在Load2及后续的读操作要读取的数据被访问前，保证Load1要读取的数据被读取完毕；

StoreStore：对于这样的语句Store1;StoreStore;Store2，在Store2及后续的写操作执行前，保证Store1的写入操作对其他处理器可见；

LoadStore：对于这样的语句Load1;LoadStore;Store2，在Store2及后续的写入操作被刷出前，保证Load1要读取的数据被读取完毕；

StoreLoad：对于这样的语句Store1;StoreLoad;Load2，在Load2及后续的读操作要读取的数据被访问前，保证Store1的写入操作对其他处理器可见；

### as if serial 单线程执行结果不变

不管如何重排序，单线程执行结果不会改变


