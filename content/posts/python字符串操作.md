---
title: "Python字符串操作"
date: 2019-09-03T11:25:09+08:00
draft: true
categories:
  - python
tags:
  - 字符串
---
<!--more-->
| 语法| 	描述
--- |  ---
| s.capitalize() |	返回字符串s的副本，并将首字符变为大写 |
| s.center(width, char)	|返回s中间部分的一个子字符串，长度为width，并使用空格或可选的char(长度为1的字符串)进行填充
s.count(t, star, end)	|返回字符串s中（或在s的start:end分片中）子字符串t出现的次数
s.encode(encoding,err)	|返回一个bytes对象，该对象使用默认的编码格式或指定编码格式来表示该字符串，并根据可选的err参数处理错误
s.expandtabs(size)	|返回s的一个副本，其中的制表符使用8个或指定数量的空格替换
s.find(t, start, end)	|返回t在s中（或在s的start:end分片中）的最左位置，如果没有找到，就返回-1，使用str:find()则可以发现相应的最右位置
s.format()	|返回按指定参数进行格式化后的字符串副本，
s.index(t, start, end) | 返回s最左边t的位置(位置或在start:end的切片中)
s.isalnum()	| 是否都为字母数字是返回true
s.isalpha()	| 是否都为字母
s.isdecimal() |	是为都为unicode的基数为10的数字
s.isdigit() |	是否全为数字
s.isidentifier()	|  是否为有效的标识符
s.islower() |	是否全为小写
s.isnumeric()	| 是否为数字或小数
s.isprintable()	| 是否为可打印的包括字符，不包括换行
s.isspace() |	是否为空白字符
s.istitle() |	是否首字母大写
s.isupper() |	是否全为大写
s.join(seq) |	返回seq中每个项链接起来后的结果
s.ljust(width, char) |	返回长度为width的字符串使用空格或可选的char进行填充
s.lower()	| 将s中的字符变为小写
s.maketrans() |	与str.translatr()类似
s.partition() |	返回包含3个字符串的远足
s.replace(t, u, n) |	替换
s.split(t, n) |	以t进行切割
s.splitlines(f) |	返回在行终结符处进行分割产生的行列表，并剥离行终结符
s.satrtwith()| 	以…开头
s.strip(char)	| 去除字符串空格
s.swapcase()  |	将大写变为小写小写转大写
s.title() |	首字母变大写
s.translate() |	
s.upper()	| 返回s分大写化版本
s.zfill(w)	| 