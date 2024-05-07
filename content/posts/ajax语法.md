---
title: "Ajax语法"
date: 2018-06-02T10:21:32+08:00
draft: false
categories:
  - ajax
---
<!--more-->
# Ajax语法

- 现在写ajax写的我很难受下面就是我在搜索的时候遇到的标签的意思

```js
$('.show_prize')获取为show_pirze的标签
.children（‘em’）获取子元素为em的标签
。text（）获取他的文本
.val() 获取他的值
parseInt  强制类型转换成整形
.toFixed(sun) 保留小数点后sun位
。click（）侦听点击事件
.blur()当输入域失去焦点 (blur
.trim()去除两边空白
.each() 方法规定为每个匹配元素规定运行的函数
find() 方法获得当前元素集合中每个元素的后代，通过选择器、jQuery 对象或元素来筛选。
.find(':checked')获取type标签的属性必须用“：”来选择
$("b").parents()查找每个 b 元素的所有父元素
change事件改变
。prop() 方法设置或返回被选元素的属性和值。
.attr()attr() 方法设置或返回被选元素的属性值。
remove()移除对应的元素
$.ajaxSettings.async = true//设置异步
$.ajaxSettings.async = false;//设置同步

```


## 全选和全不选

```js
$('.settlements').find(':checkbox').change(function () {
            //获取全选checkbox的选中状态
            is_checked = $(this).prop('checked')

            //便利所有商品对应的checkbox,设置checked属性和全选checkbox一致
            $('.cart_list_td').find(':checkbox').each(function () {
                $(this).prop('checked', is_checked)
            })
            // 更新商品信息
            update_total_price()
        });
        //商品对应的checkbox状态发生改变是，全选checkbox的改变
        $('.cart_list_td').find(':checkbox').change(function () {
            //获取所有的商品对应的chackedbox的数目
            all_len = $('.cart_list_td').find(':checkbox').length;
            //获取所有被选中的CheckBox的数目
            checked_len = $('.cart_list_td').find(':checked').length;

            if (checked_len < all_len){
                $('.settlements').find(':checkbox').prop('checked', false)
            }
            else {
                $('.settlements').find(':checkbox').prop('checked', true)
            }
            // 更新商品信息
            update_total_price1()
        })
```