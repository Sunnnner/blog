---
title: "Django Admin Permissions控制"
date: 2021-08-24T09:26:52+08:00
# weight: 1
# aliases: ["/first"]
tags: ["first"]
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


- `is_staff` bool 指定此用户是否可以访问管理站点
- 控制用户操作admin的权限由 `django.contrib.auth.backends.ModelBackend` 进行控制，它也进行控制用户的登录认证行为
-  `ModelBackend`源码解析 

```python

class ModelBackend:
    """
    Authenticates against settings.AUTH_USER_MODEL.
    """

    # 控制用户登录认证 通过重写此方法进行自定义登录认证
    def authenticate(self, request, username=None, password=None, **kwargs):
        if username is None:
            username = kwargs.get(UserModel.USERNAME_FIELD)
        try:
            user = UserModel._default_manager.get_by_natural_key(username)
        except UserModel.DoesNotExist:
            # Run the default password hasher once to reduce the timing
            # difference between an existing and a nonexistent user (#20760).
            UserModel().set_password(password)
        else:
            if user.check_password(password) and self.user_can_authenticate(user):
                return user

    # 查看用户是否为可用状态
    def user_can_authenticate(self, user):
        """
        Reject users with is_active=False. Custom user models that don't have
        that attribute are allowed.
        """
        is_active = getattr(user, 'is_active', None)
        return is_active or is_active is None

    # 获取用户的permission列表
    def _get_user_permissions(self, user_obj):
        return user_obj.user_permissions.all()

    # 获取用户的组权限列表
    def _get_group_permissions(self, user_obj):
        user_groups_field = get_user_model()._meta.get_field('groups')
        user_groups_query = 'group__%s' % user_groups_field.related_query_name()
        return Permission.objects.filter(**{user_groups_query: user_obj})

    # 获取权限列表
    def _get_permissions(self, user_obj, obj, from_name):
        """
        Return the permissions of `user_obj` from `from_name`. `from_name` can
        be either "group" or "user" to return permissions from
        `_get_group_permissions` or `_get_user_permissions` respectively.
        """
        if not user_obj.is_active or user_obj.is_anonymous or obj is not None:
            return set()

        perm_cache_name = '_%s_perm_cache' % from_name
        if not hasattr(user_obj, perm_cache_name):
            if user_obj.is_superuser:
                perms = Permission.objects.all()
            else:
                perms = getattr(self, '_get_%s_permissions' % from_name)(user_obj)
            perms = perms.values_list('content_type__app_label', 'codename').order_by()
            setattr(user_obj, perm_cache_name, {"%s.%s" % (ct, name) for ct, name in perms})
        return getattr(user_obj, perm_cache_name)

    # 获取用户权限列表
    def get_user_permissions(self, user_obj, obj=None):
        """
        Return a set of permission strings the user `user_obj` has from their
        `user_permissions`.
        """
        return self._get_permissions(user_obj, obj, 'user')

    # 获取组列表
    def get_group_permissions(self, user_obj, obj=None):
        """
        Return a set of permission strings the user `user_obj` has from the
        groups they belong.
        """
        return self._get_permissions(user_obj, obj, 'group')

    # 获取用户所有的权限列表
    def get_all_permissions(self, user_obj, obj=None):
        if not user_obj.is_active or user_obj.is_anonymous or obj is not None:
            return set()
        if not hasattr(user_obj, '_perm_cache'):
            user_obj._perm_cache = {
                *self.get_user_permissions(user_obj),
                *self.get_group_permissions(user_obj),
            }
        return user_obj._perm_cache

    # 判断是否具有权限
    def has_perm(self, user_obj, perm, obj=None):
        return user_obj.is_active and perm in self.get_all_permissions(user_obj, obj)

    # 返回某个model访问权限(True or False)
    def has_module_perms(self, user_obj, app_label):
        """
        Return True if user_obj has any permissions in the given app_label.
        """
        return user_obj.is_active and any(
            perm[:perm.index('.')] == app_label
            for perm in self.get_all_permissions(user_obj)
        )

    # 得到用户实例 (通过重写此方法或得自定义用户实例)
    def get_user(self, user_id):
        try:
            user = UserModel._default_manager.get(pk=user_id)
        except UserModel.DoesNotExist:
            return None
        return user if self.user_can_authenticate(user) else None

```


- 重写示例 

```python
class xxxBackend(ModelBackend):

    def authenticate(self, request, username=None, password=None, **kwargs):
        try:
            user = UserModel.objects.get(Q(username=username) | Q(phone=username))
            if user.check_password(password):
                return user
            return None
        except UserModel.DoesNotExist:
            return None
        except MultipleObjectsReturned:
            return None

    def get_user(self, user_id):
        try:
            return UserModel.objects.get(pk=user_id)
        except UserModel.DoesNotExist:
            return None


```