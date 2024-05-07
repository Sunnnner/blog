---
title: "Python基础"
date: 2018-06-03T10:22:36+08:00
draft: true
categories:
  - python
---

## 让python2支持中文

```python
#coding=utf-8
#-*-coding:utf-8-*-

```

- 在页面头部写入
- 变量及数据类型
- 变量就是用来存东西的
- 程序就是用来处理数据的，而变量就是用来存储数据的
- 变量起名要有意义


## 数据类型

```python
nnumber数字包括int long float complex(复数)
bollernfalse true
String
list列表（数组）
tuple元组
dictionary字典（对象）
可以用type()来查看变量数据类型
```
## 关键字
- 交换模式下使用import keyword- keyword.kwlist查看当前系统python的关键字
- python2中使用raw_iput进行获取用户键盘数据它会把任何数据当作字符串来对待
- python3中使用input来捕获用户键盘数据但是在python2中input输入的内容必须是表达式
- 输出 print


## 格式化

```python
%c代表字符
%s 通过str（）字符串转换来格式化
%i 有符号十进制整数
%d 有符号十进制整数
%u 无符号十进制整数
%o 八进制整数
%x 十六进制整数（小写字母）
%X 十六进制整数（大写字母）
%e 索引符号（小写e）
%E 索引符号（大写E）
%f 浮点实数
%g %f与%e 的简写
%G %F%E的简写
\n 换行输出
python算术运算符
+-*/
//（取整除）
%求余
** 幂
```

## 赋值运算

```python
+=
-=
*=
/=
%=
**= 幂赋值运算符
//= 取整除赋值运算符

```

## ==- while循环==

```python
complex（）创建一个复数
eval（）运算python中有效表达式并返回一个对象
tuple（）将序列s转换为一个元组
list（）转换为列表
unichr()转换为Unicode字符
ord（）转换为它的整数值
hex() 将一个整数转换为一个十六进制的字符串
oct()将一个整数转换为一个八进制字符串
```