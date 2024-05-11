---
title: "Django中的FBV和CBV"
date: 2019-09-05T11:34:25+08:00
draft: false
categories:
  - django
---
<!--more-->
## FBV

> fbv就是在url中一个路径对应一个函数

```python
urlpatterns = [
    url(r'^admin/', admin.site.urls),
    url(r'^index/', views.index)
]
```

## 视图函数中

```python
def index(request):
    return render(request, 'index.html')

```

## CBV

>cbv就是在url中一个路径对应一个类

```python
urlpatterns = [
    url(r'^admin/', admin.site.urls),
    url(r'^index/', views.IndexView.as_views()) # 执行类后面的as_view()方法
]

```


### 视图函数中

```python
from django.views import View
class IndexView(View):
    # 以get形式访问会执行get函数，一般情况下获取数据
    def get(self, *args, **keargs):
        return HttpResponse('6666')
    
    # 以post形式访问的话会执行post函数，一般情况下发送数据
    def post(self, *args, **kwargs):
        return HttpResponse('post ok')

```

## 注意:

    cbv定义类的时候必须要继承view
    在写URL的时候必须要加as_view
    类里面使用form表单提交的话只有get和post方法
    restful规范：’get’获取数据, ‘post’创建新数据, ‘put’更新, ‘patch’局部更新, ‘delete’删除, ‘head’, ‘options’, ‘trace’
## CBV重新定义dispatch函数
    所有的方法本质上都是通过dispatch这个函数反射执行，如果想要在执行get或post方法前执行其他步骤，可以重写dispatch