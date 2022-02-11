# Design Pattern

- [Design Pattern](#design-pattern)
  - [Singleton](#singleton)
    - [**饿汉式**](#饿汉式)
    - [**懒汉式 lazy loading**](#懒汉式-lazy-loading)

- [主页](README.md)

## Singleton

单例模式，采取一定方法保证整个软件系统中，对某个类只能存在一个对象实例

### **饿汉式**

优点：类加载到内存以后，就是理化一个单例，避免线程同步问题，JVM保证线程安全

缺点：类装载时就完成实例化，如果未使用这个实例，则造成内存浪费

```java
public class singleton {
    public static void main(String[] args) {
        SingletonStaticVariable instance = SingletonStaticVariable.getInstance();
        SingletonStaticVariable instance2 = SingletonStaticVariable.getInstance();
        System.out.println(instance == instance2);
    }
}

class Singleton {
private Singleton() {

}

private static final Singleton instance = new Singleton();

/*
# 用静态语句块

private static final Singleton instance；

static {
    instance = new Singleton();
}
*/

public static Singleton getInstance() {
    return instance;
}

```

### **懒汉式 lazy loading**

优点：达到了按需初始化的目的

缺点：带来线程不安全问题，因此加上synchronized保证线程安全，但同时效率降低

```java
public class singleton04 {
    private static singleton04 INSTANCE;
    
    public static synchronized singleton04 singleton04() {
        if (INSTANCE == null) {
            INSTANCE = new singleton04();
        } 
        return INSTANCE;
    }
}
```

因此在判断的时候上锁，并加上两次判断实现效率提升

```java
public class singleton05 {
    private static volatile singleton05 INSTANCE;
    
    private singleton05(){
        
    }

    public static singleton05 getInstance() {
        if (INSTANCE == null) {
            synchronized (singleton05.class) {
                if (INSTANCE == null)
                    INSTANCE = new singleton05();
            }
        }
        return INSTANCE;
    }
}
```

改进饿汉式写法，加载外部类的时候不会加载内部类，可实现懒加载

```java
public class singleton06 {

    private singleton06(){

    }

    private static class singleton06Holder {
        private final static singleton06 INSTANCE = new singleton06();
    }
    public static singleton06 getInstance() {
        return singleton06Holder.INSTANCE;
    }

}
```

effective java中枚举单例写法，不仅可解决线程同步，还可以防止反序列化（因为没有构造方法）。

```java
public enum singleton07 {
    INSTANCE;
    
    public void m() {
    }
}
```


