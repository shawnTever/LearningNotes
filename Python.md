# Python

- [Python](#python)
  - [解释型语言和编译型语言](#解释型语言和编译型语言)
  - [Python运行过程](#python运行过程)
  - [Python的作用域](#python的作用域)
  - [Python的数据结构](#python的数据结构)
  - [Python可变与不可变类型](#python可变与不可变类型)

- [主页](README.md)

## 解释型语言和编译型语言

编译型语言：编译型语言在执行之前要先经过编译过程，编译成为一个可执行的机器语言的文件.

解释型语言：解释性语言编写的程序不进行预先编译，以文本方式存储程序代码。

## Python运行过程

编译与运行：

源代码.py被编译成字节码，然后由PVM虚拟机运行

生成的字节码，会被保存到当前目录下的__pycache__中，命名为*.pyc

## Python的作用域

- L （Local） 局部作用域
- E （Enclosing） 闭包函数外的函数中
- G （Global） 全局作用域
- B （Built-in） 内建作用域

变量以 L –> E –> G –>B 的规则查找

## Python的数据结构

Python中内置的数据结构有六种:Number (数值)、String (字符串)、list (列表)、Tuple(元组),Dictionary (字典)、Set (集合)，除此以队外，数组、矩阵等结构需要导入工具包后才可以实现。

## Python可变与不可变类型

可变：列表、集合、字典

不可变：字符串、元组、数字
