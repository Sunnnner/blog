---
title: "Python模板库mako语法"
date: 2023-03-10T15:46:40+08:00
draft: false
categories:
  - python
tags:
  - mako
---

<!--more-->

*   表达式替换 this is x:\${x}
*   \${}里面的内容由Python直接计算，因此可以以使用完整的表达式
*   pythagorean theorem ：\${pow(x, 2) + pow(y, 2)}
*   表达式的结果都会在输出到输出流之前转换为字符串形式

***

*   表达式转义
*   \${"this is some text" | u}
*   上面讲URL转义应用到表达式上，生成this+is+some+text，u表示URL转义，h表示HTML转义，x表示xml转义，trim 为空白截断函数

***

*   控制结构
*   mako中控制结构写成%标记后面跟正常的Python控制表达式，用%加标签end\<name> 结束,\<name>为关键词

***

*   例子
```python
%for x in range(10):
\${x}
%endfor
```
