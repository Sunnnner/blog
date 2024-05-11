---
title: "Go学习"
date: 2020-02-01T15:45:32+08:00
draft: false
categories:
  - go
---
<!--more-->

# Go关键字

关键字	| 意义
--- | ---
break	| 退出
default	| 默认函数
func	| 定义函数和方法
interface	| 用于定义接口
select	| 用于选择不同类型的通讯
case	| 用户条件选择
defer	| 延迟执行内容（收尾工作）有点类似C++的析构，但是它是再函数结尾的时候去执行（也就是栈即将被释放的时候）
go	| 用于并发
map	| 用于声明map类型数据
struct	| 用于定义抽象数据类型
range	| 用于读取slice、map、channel数据
chan	| 用于channel通讯
if	| 选择结构-如果
else	| 选择结构-否则
type	| 用于声明自定义类型
return	| 用于从函数返回
var	| Go语言基础里面的变量和常量申明 (var age int)
const	| 变量和常量的声明
package	| 包管理
import	| 导入
switch	| 选择结构
fallthrough	| 流程控制</br>1.加了fallthrough后，会直接运行【紧跟的后一个】case或default语句，不论条件是否满足都会执行)</br>2.加了fallthrough语句后，【紧跟的后一个】case条件不能定义常量和变量</br>3.执行完fallthrough后直接跳到下一个条件语句，本条件执行语句后面的语句不执行
continue	| 跳过本次循环
for	| 循环
goto	| 跳转语句

## 36个预定义标识符

内建常量	| 内建类型	| 内建函数
--- | --- | ---
true	| int	| make
false	| int8	| len
iota	| int16	| cap
nil	| int32	| new
| -	| int64	| append
| -	| uint	| copy
| -	| uint8	| close
| -	| uint16	| delete
| -	| uint32	| complex
| -	| uint64	| real
| -	| uintprt	| imag
| -	| float32	| panic
| -	| float64	| recover
| -	| complex64	| -
| -	| complex128 |	-
| -	| bool	| -
| -	| byte	| -
| -	| rune	| -
| -	| string |	-
| -	| error	| -

![xx](/img/go.jpg)