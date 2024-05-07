---
title: "修改macos自带Python版本（尽量不要修改）"
date: 2019-09-02T11:24:14+08:00
draft: true
categories:
  - python
tags:
  - macos
---
<!--more-->
```text

1.在下载最新python（3.6）：wget https://www.python.org/ftp/python/3.6.1/python-3.6.1-macosx10.6.pkg
2.安装python-3.6.1-macosx10.6.pkg
3.删除mac自带的python2.7：
sudo rm -R /System/Library/Frameworks/Python.framework/Versions/2.7 
4.把刚安装好的python移到原本系统python位置：

sudo mv /Library/Frameworks/Python.framework/Versions/3.6 /System/Library/Frameworks/Python.framework/Versions
5.修改文件所属的Group，设置Group为wheel：

sudo chown -R root:wheel /System/Library/Frameworks/Python.framework/Versions/3.6```
6.更新Current的Link
sudo rm /System/Library/Frameworks/Python.framework/Versions/Current
sudo ln -s /System/Library/Frameworks/Python.framework/Versions/3.6 /System/Library/Frameworks/Python.framework/Versions/Current

7.删掉原来的执行文件
sudo rm /usr/bin/pydoc
sudo rm /usr/bin/python
sudo rm /usr/bin/pythonw
sudo rm /usr/bin/python-config
sudo rm /usr/bin/easy_install
sudo rm /usr/bin/pyvenv

8.建立新的链接
sudo ln -s /System/Library/Frameworks/Python.framework/Versions/3.6/bin/pydoc3.6 /usr/bin/pydoc
sudo ln -s /System/Library/Frameworks/Python.framework/Versions/3.6/bin/python3.6 /usr/bin/python
sudo ln -s /System/Library/Frameworks/Python.framework/Versions/3.6/bin/pythonw3.6 /usr/bin/pythonw
sudo ln -s /System/Library/Frameworks/Python.framework/Versions/3.6/bin/python3.6m-config /usr/bin/python-config
sudo ln -s /System/Library/Frameworks/Python.framework/Versions/3.6/bin/pip3.6 /usr/bin/pip
sudo ln -s /System/Library/Frameworks/Python.framework/Versions/3.6/bin/easy_install-3.6 /usr/bin/easy_install
sudo ln -s /System/Library/Frameworks/Python.framework/Versions/3.6/bin/pyvenv-3.6 /usr/bin/pyvenv

9.添加环境变量
创建.bash_profile：`touch .bash_profile`
vim命令打开.bash_profile：`vim .bash_profile`
添加环境变量：
Setting PATH for Python 3.6
The orginal version is saved in .bash_profile.pysave
PATH="/System/Library/Frameworks/Python.framework/Versions/3.6/bin:${PATH}"
export PATH
`alias python="python3.6"

source .bash_profile`

11.测试是否成功：
  输入python命令，查看版本python

```