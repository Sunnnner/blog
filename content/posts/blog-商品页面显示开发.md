---
title: "页面开发"
date: 2018-05-31T18:47:29+08:00
draft: true
categories:
  - django
tags:
  - django

---
<!--more-->
- 首先新建app—>books并添加settings里面
- 因为我们需要在后台admin上传数据所以我们要创建富文本管理器并在setting设置他的选项
- 富文本管理器是一个插件我们这次使用的是tinymce并且我们需要将它加入到apps里面因为他是一个应用，但是这个应用是需要下载的

```python
TINTMCE_DEFAULT_CONFIG = {
    'theme': "modern",
    'wight': 600,
    'height': 400,
}
```

- 我们需要设置制定一个媒体文件夹来存放我们的图片`MEDIA_ROOT = os.path.join(BASE_DIR, 'static')`

- 添加应用的urls``

```python
url(r'^books/', include('books.urls',namespace='books')),
url(r'^tinymce/', include('tinymce.urls',namespace='tinymce')),
```

- 我们开始写books里面的字段首先查看页面我们需要什么字段
- 首先我们创建tinymac富文本需要的字段，这里的字段映射全局
- 在books目录下创建任意的.py文件这里我的是emums.py

```python
# 此处1，2，3，4代表书本的id
PYTHON = 1
JAVASCRIPT = 2
ALGORITHMS = 3
MACHINELEARNING = 4
OPERATINSGYSTEM = 5
DATABASE = 6

# BOOKS_TYPE作为一个字典传输到models
BOOKS_TYPE = {
    PYTHON: 'python',
    JAVASCRIPT: 'javascript',
    ALGORITHMS: '数据库结构与算法',
    MACHINELEARNING: '机器学习',
    OPERATINSGYSTEM: '操作系统',
    DATABASE: '数据库',

}

# 代表商品的上线或者下线状态
OFFLINE = 0
ONLINE = 1

STATUS_CHOICE = {
    OFFLINE: '下线',
    ONLINE: '上线',
}
```

- 我们开始写models.py

```python
from django.db import models
from db.base_model import BaseModel
from tinymce.models import HTMLField
from books.enums import BOOKS_TYPE, STATUS_CHOICE,PYTHON,ONLINE

# Create your models here.

class BookManager(models.Manager):
    '''商品模型管理器类'''
    # type_id 表示前段传输商品id进行查找商品. limit表示返回几个之前的商品的数据, sort代表排序状态，初始值默认
    def get_books_by_type(self, type_id, limit=None, sort='default'):
        '''根据商品类型id查询商品信息'''
        # 如果是新商品就根据他的添加时间进行排序-代表从大到小进行排序
        if sort == 'new':
            order_by = ('-create_time',)
        # 根据销量最多进行排序
        elif sort == 'hot':
            order_by = ('-sales',)
        # 根据价格进行排序
        elif sort == 'price':
            order_by = ('price',)
        else:
        # pk国外代表一种主键的简写，别的名字也行这是整个表的主键，这里代表的意思就是默认按照主键primary_key从大到小默认进行排序
            order_by = ('-pk',)
        # 查询数据 filter是过滤数据，order_by是排序，(*order_by)是对上面的order_by进行解包成列表
        # 对解包的数据进行过滤排序并返回一个新的列表books_li
        books_li = self.filter(type_id=type_id).order_by(*order_by)

        # 查询结果集的限制
        if limit:
            books_li = books_li[:limit]
        return books_li

    def get_books_by_id(self, books_id):
        '''根据商品id获取商品信息'''
        try:
            books = self.get(id=books_id)
        except self.model.DoesNotExist:
            # 商品不存在
            books = None
        return books

class Books(BaseModel):
    '''商品模型类'''
    # 使用迭代器进行数据赋值 因为books_type是字典所以要取items
    books_type_choices = ((k, v) for k, v in BOOKS_TYPE.items())
    status_choices = ((k, v) for k, v in STATUS_CHOICE.items())
    # 定义书籍的id与书籍的状态
    type_id = models.SmallIntegerField(default=PYTHON, choices=books_type_choices,verbose_name='商品种类')
    name = models.CharField(max_length=20, verbose_name='商品名称')
    desc = models.CharField(max_length=128, verbose_name='商品简介')
    # decimal_places代表小数后两位
    price = models.DecimalField(max_digits=10, decimal_places=2, verbose_name='商品价格')
    unit = models.CharField(max_length=20, verbose_name='商品单位')
    stock = models.IntegerField(default=1, verbose_name='商品库存')
    sales = models.IntegerField(default=0, verbose_name='商品销量')
    detail = HTMLField(verbose_name='商品详情')
    # upload_to所以可以用uoload_to来指定文件存放的前缀路径
    # 实际的路径就是 MEDIA_ROOT/books/filename
    image = models.ImageField(upload_to='books', verbose_name='商品图片')
    status = models.SmallIntegerField(default= ONLINE, choices=status_choices,verbose_name='商品状态')

    def __str__(self):
        return self.name
    # 创建事务管理器
    object = BookManager()

    class Meta():
        #制定数据库名称
        db_table = 's_books'
```

- 将用户模块注册到admin

```python
from django.contrib import admin
from books.models import Books
# Register your models here.

admin.site.register(Books)
```

- 创建用户主页视图views信息

```python
from django.shortcuts import render,redirect
from books.models import Books
from books.enums import *
from django.core.urlresolvers import reverse
from django.core.paginator import Paginator
# Create your views here.


def index(request):
    '''显示首页'''
    python_new = Books.object.get_books_by_type(PYTHON, 3, sort='new')
    python_hot = Books.object.get_books_by_type(PYTHON, 4, sort='hot')
    javascript_new = Books.object.get_books_by_type(JAVASCRIPT, 3, sort='new')
    javascript_hot = Books.object.get_books_by_type(JAVASCRIPT, 4, sort='hot')
    algorithms_new = Books.object.get_books_by_type(ALGORITHMS, 3, sort='new')
    algorithms_hot = Books.object.get_books_by_type(ALGORITHMS, 4, sort='new')
    machinelearning_new = Books.object.get_books_by_type(MACHINELEARNING, 3,sort='new')
    machinelearning_hot = Books.object.get_books_by_type(MACHINELEARNING, 4, sort='hot')
    operatingsystem_new = Books.object.get_books_by_type(OPERATINSGYSTEM, 3, sort='new')
    operatingsystem_hot = Books.object.get_books_by_type(OPERATINSGYSTEM, 4, sort='hot')
    database_new = Books.object.get_books_by_type(DATABASE, 3, sort='new')
    database_hot = Books.object.get_books_by_type(DATABASE, 4, sort='hot')

    # 定义模板上下文
    content = {
        'python_new': python_new,
        'python_hot': python_hot,
        'javascript_new': javascript_new,
        'javascript_hot': javascript_hot,
        'algorithms_new': algorithms_new,
        'algorithms_hot': algorithms_hot,
        'machinelearning_new': machinelearning_new,
        'machinelearning_hot': machinelearning_hot,
        'operatingsystem_new': operatingsystem_new,
        'operatingsystem_hot': operatingsystem_hot,
        'database_new': database_new,
        'database_hot': database_hot,
    }
    return render(request, 'index.html', content)
```

- 创建商品详情页
- 首先创建url`url(r'^(?P<books_id>\d+)/$',deatil,name='deatil')`
- 创建视图

```python
def deatil(request, books_id):
    '''显示商品的详细信息'''
    books = Books.object.get_books_by_id(books_id=books_id)

    if books is None:
        return redirect(reverse('index'))

    # 新品推荐
    books_li = Books.object.get_books_by_type(type_id=books.type_id, limit=2, sort='new')

    # 定义返回数据
    content = {
        'books': books,
        'books_li': books_li,
    }
    return render(request, 'detail.html', content)
```

- 设置前端显示模板语言
