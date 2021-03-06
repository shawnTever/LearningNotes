# SQL

- [SQL](#sql)
  - [limit 限制查询结果返回数量](#limit-限制查询结果返回数量)
  - [delete删除表中记录](#delete删除表中记录)
  - [in和exists区别](#in和exists区别)
  - [int(20)中20的涵义](#int20中20的涵义)
  - [UNION与UNIONALL的区](#union与unionall的区)
  - [asc 升序, desc 降序](#asc-升序-desc-降序)
  - [什么是索引？](#什么是索引)
  - [索引使用场景](#索引使用场景)
    - [orderby](#orderby)
    - [join](#join)
  - [索引查询方式](#索引查询方式)
  - [drop、delete与truncate的区别](#dropdelete与truncate的区别)
  - [事务的四大特性（ACID）](#事务的四大特性acid)
  - [MySQL数据库四种隔离级别](#mysql数据库四种隔离级别)
  - [数据库的脏读、幻读、不可重复读](#数据库的脏读幻读不可重复读)
  - [Mybatis中#与$区别](#mybatis中与区别)
  - [共享锁和排它锁](#共享锁和排它锁)
  - [悲观锁和乐观锁](#悲观锁和乐观锁)

- [主页](README.md)

## limit 限制查询结果返回数量

limit有两种方式。

limit a,b 后缀两个参数的时候，其中a是指记录开始的偏移量,b是指从第a+1条开始，取b条记录

limit b 后缀一个参数的时候，是直接取值到第多少位,类似于：limit 0,b

e.g. SELECT * FROM table LIMIT 5,10;  检索记录行 6-15

SELECT * FROM table LIMIT 95,-1; 检索记录行 96-last

## delete删除表中记录

DELETE FROM <表名> [WHERE 子句] [ORDER BY 子句] [LIMIT 子句]

<表名>：指定要删除数据的表名。

ORDER BY 子句：可选项。表示删除时，表中各行将按照子句中指定的顺序进行删除。

WHERE 子句：可选项。表示为删除操作限定删除条件，若省略该子句，则代表删除该表中的所有行。

LIMIT 子句：可选项。用于告知服务器在控制命令被返回到客户端前被删除行的最大值。

## in和exists区别

select * from A
where id in(select id from B)

select * from A
where id exists(select id from B)

in语句是把外表和内表作hash连接，而exists语句是对外表作loop

1. in()适合A表比B表数据大的情况，in用的是hash join，所以内表B如果小，整个查询的范围都会很小，速度快，如果内表B大查询范围大，速度就会很慢。

2. exists()适合A表比B表数据小的情况，因为循环的次数对于exists影响最大，所以，外表A要记录数少，内表B记录要大。
  
3. not in 和not exists：如果查询语句使用了not in，那么内外表都进行全表扫描，没有用到索引；而not extsts的子查询依然能用到表上的索引。所以无论那个表大，用not exists都比not in要快。

## int(20)中20的涵义

20表示显示字符的长度宽为20，但仍占4字节存储。不影响内部存储，只是影响带 zerofill 定义的 int 时，前面补多少个0。

## UNION与UNIONALL的区

如果使用UNION ALL，不会合并重复的记录行，效率 UNION 高于 UNION ALL

## asc 升序, desc 降序

asc 按升序排列 (不用写，默认使用这个)desc 按降序排列

## 什么是索引？

包含着对数据表里所有记录的引用指针，索引的实现通常使用B树及其变种B+树。

## 索引使用场景

### orderby

当我们使用orderby将查询结果按照某个字段排序时，如果该字段没有建立索
引，那么执行计划会将查询出的所有数据使用外部排序。

### join

对join语句匹配关系（on）涉及的字段建立索引能够提高效率。

## 索引查询方式

主键索引区:PI(关联保存的时数据的地址)按主键查询,

普通索引区:si(关联的id的地址,然后再到达上面的地址)。所以按主键查询,速度快

## drop、delete与truncate的区别

在不再需要一张表的时候，用drop；

在想删除部分数据行时候，用 delete；

在保留表而删除所有数据的时候用truncate

## 事务的四大特性（ACID）

1. 原子性（Atomicity）

原子性是指事务包含的所有操作要么全部成功，要么全部失败回滚，这和前面两篇博客介绍事务的功能是一样的概念，因此事务的操作如果成功就必须要完全应用到数据库，如果操作失败则不能对数据库有任何影响。

2. 一致性（Consistency）

一致性是指事务必须使数据库从一个一致性状态变换到另一个一致性状态，也就是说一个事务执行之前和执行之后都必须处于一致性状态。

拿转账来说，假设用户A和用户B两者的钱加起来一共是5000，那么不管A和B之间如何转账，转几次账，事务结束后两个用户的钱相加起来应该还得是5000，这就是事务的一致性。

3. 隔离性（Isolation）

隔离性是当多个用户并发访问数据库时，比如操作同一张表时，数据库为每一个用户开启的事务，不能被其他事务的操作所干扰，多个并发事务之间要相互隔离。

即要达到这么一种效果：对于任意两个并发的事务T1和T2，在事务T1看来，T2要么在T1开始之前就已经结束，要么在T1结束之后才开始，这样每个事务都感觉不到有其他事务在并发地执行。

关于事务的隔离性数据库提供了多种隔离级别，稍后会介绍到。

4. 持久性（Durability）

持久性是指一个事务一旦被提交了，那么对数据库中的数据的改变就是永久性的，即便是在数据库系统遇到故障的情况下也不会丢失提交事务的操作。

例如我们在使用JDBC操作数据库时，在提交事务方法后，提示用户事务操作完成，当我们程序执行完成直到看到提示后，就可以认定事务以及正确提交，即使这时候数据库出现了问题，也必须要将我们的事务完全执行完成，否则就会造成我们看到提示事务处理完毕，但是数据库因为故障而没有执行事务的重大错误。

## MySQL数据库四种隔离级别

1. Serializable (串行化)：可避免脏读、不可重复读、幻读的发生。

2. Repeatable read (可重复读)：可避免脏读、不可重复读的发生。

3. Read committed (读已提交)：可避免脏读的发生。

4. Read uncommitted (读未提交)：最低级别，任何情况都无法保证。

## 数据库的脏读、幻读、不可重复读

**脏读**：指一个事务A正在访问数据，并且对该数据进行了修改，但是这种修改还没有提交到数据库中。这时候另外一个事务B也访问这个数据，然后使用了这个被A修改的数据，那么这个数据就是脏的，并不是数据库中真实的数据。

**幻读**：是指当事务不是独立执行时发生的一种现象,系统管理员A将数据库中所有学生的成绩从具体分数改为ABCDE等级，但是系统管理员B就在这个时候插入了一条具体分数的记录，当系统管理员A改结束后发现还有一条记录没有改过来，就好像发生了幻觉一样。这就叫幻读。

**不可重复读**：不可重复读是指在同一个事务内，两个相同的查询返回了不同的结果。例如：事务T1读取某一数据，事务T2读取并修改了该数据，T1为了对读取值进行检验而再次读取该数据，便得到了不同的结果

## Mybatis中#与$区别

\#{变量名}会转化为jdbc的类型。

${变量名}不进行数据类型匹配，直接替换。

\#方式能够很大程度防止sql注入。

## 共享锁和排它锁

共享锁: 又叫做读锁。 当用户要进行数据的读取时，对数据加上共享锁。共享锁可以同时加上多个。
排他锁: 又叫做写锁。 当用户要进行数据的写入时，对数据加上排他锁。排他锁只可以加一个，他和其他的排他锁，共享锁都相斥。

## 悲观锁和乐观锁

悲观锁：假定会发生并发冲突，屏蔽一切可能违反数据完整性的操作。在查询完数据的时候就把事务锁起来，直到提交事务。

乐观锁：假设不会发生并发冲突，只在提交操
作时检查是否违反数据完整性。
