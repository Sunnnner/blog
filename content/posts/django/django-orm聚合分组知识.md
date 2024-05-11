---
title: "Django Orm聚合分组知识"
date: 2021-08-12T16:19:36+08:00
draft: false
categories:
  - django
tags:
  - orm

---
<!--more-->


- `annotate` 聚合操作 有 Max Sum Count一些参数使用 `=`相当于sql中的`as`
- 如果想要查询的时候更换变量名称使用`extra(select={"change_file": "model_file"})` 相当于 sql 中的`as`
- sql中`order by`分组在orm使用`values`进行表达
- 示例

```python
# 按照各个省事进行聚合数量
DemoModel.objects.filter(test=xxx).extra(select={'position': city}).\
            values("position", "location").annotate(count=Count(city))

```



