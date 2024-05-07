---
title: "Shell if Then语句"
date: 2019-08-19T11:21:38+08:00
draft: true
categories:
  - shell
---
<!--more-->
```shell
! /bin/bash
this is an example of a if -then


if-then比较整数
score=91
if (("$score">90))

then
    echo "well done"
fi

if-then 比较字符串

word=abc

if [$word="abc"]

then
    echo "condition is true"
fi

if-then-else

word=abc

if [ $word='abccccc' ]

then
    echo 'f'
else
    echo 'false'
fi

if-then-elif-then-else

num=6
if (($num>7))
then
    echo '6 is bigger'
elif (($num<7))
then
    echo '7 is bigger'
else
    echo 'nonoooo'
fi

整数比较符
 
-eq	: (equal to)相等          		    例如： if [ "$a" -eq "$b"  ]
-ne	: (not equal to)相等      		    例如： if [ "$a" -ne "$b"  ]
-gt	: (greater than)大于      		    例如： if [ "$a" -gt "$b"  ]
-ge	: (greater than or equal to)大于或等于      例如： if [ "$a" -ge "$b"  ]
-lt	: (less than)小于                           例如： if [ "$a" -lt "$b"  ]
-le	: (less than or equal to)小于或等于         例如： if [ "$a" -le "$b"  ]
<	: 小于                                      例如： if (( "$a" < "$b" ))
<=	: 小于等于                                  例如： if (( "$a" <= "$b" ))
>	: 大于                                      例如： if (( "$a" > "$b" ))
>=	: 大于等于                                  例如： if (( "$a" >= "$b" ))
 
字符串比较
 
=	: 等于                                      例如： if [ "$a" = "$b"   ]
==	: 等于                                      例如： if [ "$a" == "$b"  ]
!=	: 不等于                                    例如： if [ "$a" != "$b"  ]
<	: 小于（ASCII字母顺序）                     例如： if [[ "$a" < "$b" ]]
>	: 大于（ASCII字母顺序）                     例如： if [[ "$a" > "$b" ]]
-z	: 字符不为空                

需要注意，什么时候用单个中括号和两个中括号，还有什么时候使用两个小括号，注意括号内空格。
```
