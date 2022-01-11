# Design Pattern

- [Design Pattern](#design-pattern)
  - [Singleton](#singleton)
    - [饿汉式](#饿汉式)

- [主页](README.md)

## Singleton

单例模式，采取一定方法保证整个软件系统中，对某个类只能存在一个对象实例

### 饿汉式

优点：类加载到内存以后，就是理化一个单例，避免线程同步问题，JVM保证线程安全

缺点：类装载时就完成实例化，如果未使用这个实例，则造成内存浪费

    class SingletonStaticVariable {
    private SingletonStaticVariable() {

    }

    private final static SingletonStaticVariable instance = new SingletonStaticVariable();

    public static SingletonStaticVariable getInstance() {
        return instance;
    }



