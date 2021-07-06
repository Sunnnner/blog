---
title: "Django用户模块"
date: 2018-06-01T10:15:16+08:00
draft: true
# weight: 1
# aliases: ["/first"]
tags: ["django"]
author: "whitek"
showToc: true
TocOpen: false
draft: false
hidemeta: false
comments: false
description: "Desc Text."
disableHLJS: true # to disable highlightjs
disableShare: false
disableHLJS: false
hideSummary: false
searchHidden: true
ShowReadingTime: true
ShowBreadCrumbs: true
ShowPostNavLinks: true
cover:
    image: "<image path/url>" # image path/url
    alt: "<alt text>" # alt text
    caption: "<text>" # display caption under cover
    relative: false # when using page bundles set this to true
    hidden: true # only hide on current single page
editPost:
    URL: "https://github.com/Sunnnner/Sunnnner.github.io/content"
    Text: "Suggest Changes" # edit text
    appendFilePath: true # to append file path to Edit link
---

# 第一步创建Django项目
- `django-admin startproject blog`

## 创建第一个应用user

- `python manage.py startapp user`

## 设置setting文件

```python
ALLOWED_HOSTS=[“*”]//更改为所有都可以访问上线模式
INSTALLEN_APPS—》加入第一个user应用
```

- 创建templates文件夹 并设置TEMPLATES里面文件夹的路径os.path.join
- 设置DATABASES的储存为mysql

```python
字段
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'NAME': 'bookstore',
        'USER':'root',
        'PASSWORD':'123',
        'HOST':'localhost',
        'PORT':3306,
    }
}
```

## 修改语言与时区

```python
LANGUAGE_CODE = 'zh-Hans'

TIME_ZONE = 'Asia/Shanghai'

```

## 设置静态文件收集static文件夹并在setting设置

```python
STATIC_URL = '/static/'
STATICFILES_DIRS = [
    os.path.join(BASE_DIR, 'static')
]
```


## 设置主页url与视图函数

```python
url(r'^$',index,name='index')
def index(request):
    return render(request, 'index.html')

```

## 编写用户模块
## 编写注册模块

- 首先编写抽象类，所谓抽象类就是所有类模板都能用上的类
- 在根目录创建`db pythonFile`文件夹

## 创建base_model抽象基类抽象基类继承models.Model

```python
from django.db import models
class BaseModel(models.Model):
    '''模型抽象基类'''
    is_delete = models.BooleanField(default=False, verbose_name='是否删除')
    create_time = models.DateTimeField(auto_now_add=True, verbose_name='创建时间')
    update_time = models.DateTimeField(auto_now=True, verbose_name='更新时间')

    class Meta:
        # 继承抽象类
        abstract = True
```


- 根目录创建utils文件夹该文件夹的作用作为加密用户密码
- 创建get_hash文件夹

```python
from hashlib import sha256

def get_hash(str):
    '''取一个字符串的hash值'''
    sh = sha256
    sh.update(str.encode('utf8'))
    return sh.hexdigest()
```

- 打开app内的models模块开始编写用户模块
- 导入get_hash函数
- 导入抽象基类
- 创建用户字段使其继承与抽象基类
- 其中db_table的作用为制定创建数据库的名称

```python
class Passport(BaseModel):
    username = models.CharField(max_length=20,verbose_name='用户名称',unique=True)
    password = models.CharField(max_length=40,verbose_name='用户密码')
    email = models.EmailField(verbose_name='用户邮箱')
    is_active = models.BooleanField(default=False, verbose_name='激活状态')

    # 创建用户表的管理器
    object = PassportManager()

    class Meta():
        # 指定数据库名称
        db_table = 's_user_accoumt'
```

- 创建添加用户跟查找用户模块注意此字段必须在用户模块的上方因为此字段继承的model.Manager模块在用户模块之上

```python
class PassportManager(models.Manager):

    def add_user(self,username, password, email):
        '''添加一个用户信息'''
        # s使用crate方法添加一个用户
        passport = self.create(username=username, password=get_hash(password), email=email)

        # 并且返回当前的数据
        return passport

    def find_user(self,username, password):
        '''根据用户的信息进行查找用户'''
        try:
            passport = self.get(username=username, password=get_hash(password))
        except self.model.DoesNotExist:
            # 账户不存在
            print("=======")
            passport = None
        # 返回当前的信息
        return passport
```


- 创建完成之后python3 manage.py makemigrations迁移同步
- 编写用户注册视图函数

```python
url(r’^/register/$’, register, name=’register’),
def register(request):
    if request.method == 'GET':
        return render(request,'register.html')

    else:
        username = request.POST.get('user_name')
        password = request.POST.get('pwd')
        password1 = request.POST.get('cpwd')
        email = request.POST.get('email')
        # all方法进行数据校验，如果里面任意值为空，就不通过校验
        if not all([username,password,password1,email]):
            return render(request, 'register.html', {
                'msg':'不能输入有空的参数'
            })
        # 邮箱正则验证
        if not re.match(r'[a-z0-9][\w\.\-]*@[a-z0-9\-]+(\.[a-z]{2,5}){1,2}$', email):
            return render(request, 'register.html', {'msg':'输入的邮箱不正确'})

        # 通过向数据库添加用户信息
        # 调用添加用户的方法
        passport = Passport.object.add_user(username=username, password=password, email=email)
        
        return redirect(reverse('user:register'), {'cmsg':'注册成功'})
```

## 创建登录模块
- url(r’^login/$’, login, name=’login’),
- 因为登录模块用到ajax 所以我们先写前端数据
- 首先ajax传输不用表单数据我们就删除from表单

```html
<div class="form_input">
    {% csrf_token %}
	<input type="text" id="username" value="{{ username }}" class="name_input" placeholder="请输入用户名">
	<div class="user_error">输入错误</div>
	<input type="password" id="pwd" class="pass_input" placeholder="请输入密码">
	<div class="pwd_error">输入错误</div>
	<div class="more_input clearfix">
		<input type="checkbox" id="remember" checked={{ checked }}>
		<label>记住用户名</label>
		<a href="#">忘记密码</a>
	</div>
	<input type="button" id="btnLogin" value="登录" class="input_submit">

</div>
AJAX
<script src="{% static 'js/jquery-1.12.4.min.js' %}"></script>
    <script>
        $(function () {
            $('#btnLogin').click(function () {
                //获取用户名和密码
                # 使用jquay获取用户的信息
                var username = $('#username').val();
                var password = $('#pwd').val();
                # 设置csrf_token为标签设置其属性name=csrfmiddlewaretoken并将获取到的cdrf_token的值赋值给csrf
                var csrf = $('input[name="csrfmiddlewaretoken"]').val();
                # 返回当前记住用户的状态true/false
                var remember = $('#remember').prop('checked');

                //发起ajax请求
                params = {'username':username, 'password':password,
                'csrfmiddlewaretoken':csrf, 'remember':remember};
                //ajax将python字典转换为了json字符串型字典此时类型为json类型
                $.post('{% url "user:login" %}', params, function(data){
                    //用户名密码错误{'res':0}
                    //登录成功{'res':1}
                    //状态码状态码为01，2
                    if (data.res == 0) {
                        alert('用户名或者密码错误')
                    }
                    else if(data.res == 1)
                        {
                            //跳转页面  获取后端next_url
                            location.href = data.next_url
                        }
                    else if(data.res == 2)
                    {
                        alert('请填写完整的用户名或者密码')
                    }
                })
            })
        })
    </script>

```

## 后端代码

- 用户登录校验

```python
def login(request):
    if request.method == 'GET':
        # 记住用户名功能 checked表示单选框状态
        if request.COOKIES.get("username"):
            username = request.COOKIES.get("username")
            checked = True
        else:
            username = ''
            checked = ''
        context = {
            'username': username,
            'checked' : checked,
        }
        return render(request, 'login.html', context)
    elif request.method == 'POST':
        # 此时post取的是前段ajax数据并不是表单数据因为表单已经删除
        username = request.POST.get('username')
        password = request.POST.get('password')
        remember = request.POST.get('remember')

        # 数据校验 使用all()方法进行校验只有两个都不为空时才为true
        if not all([username, password]):
            # 数据为空 返回ajax里面的状态码json数据
            return JsonResponse({'res': 2})
        # 调用查找方法判断用户是否存在
        passport = Passport.object.find_user(username=username,password=password)

        if passport:
            # 两种方法都是重定向到主页
            # next_url = request.session.get('url_path', reverse('index'))
            next_url = '/'
            print('---------------')
            # 登录成功 返回状态码并设置next_url数据传输到前段都是字典模式会自动转换成json字符串
            jire = JsonResponse({'res': 1, 'next_url': next_url})
            # 如果单选框选中
            if remember == 'true':
                # 记住用户名并设置cookie的保存时间
                jire.set_cookie('username', username, max_age=1*24*3600)
            else:
                # 不要记住用户名并删除cookie
                jire.delete_cookie('username')
            # 记住用户名的状态
            # 设置是否登录状态前段要用用session保存到服务器
            request.session['islogin'] = True
            request.session['username'] = username
            # 当前用户的唯一标示
            request.session['passport_id'] = passport.id
            return jire
        else:

            return JsonResponse({'res': 0})
```


## 退出

```python
url(r’^logout/$’, logout, name=’logout’),
def logout(request):
    '''用户退出操作'''
    # 清空用户session数据
    request.session.flush()
    # 然后跳转首页
    return redirect(reverse('index'))
```