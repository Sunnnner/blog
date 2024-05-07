---
title: "Rclone挂载googleDrive"
date: 2019-09-04T11:30:51+08:00
draft: false
categories:
  - linux
tags:
  - rclone
---
<!--more-->
- 最近查找大容量存储工具，想到了免费版的Google云盘，询问了一下有一个无限空间的云盘，话不多说开始搞，在淘宝买了个账号开始配在自己的服务器上，但是发现并不是这么好配，查找了很多资料，到最后朋友给我说rclone可以挂在Google云盘，查了一下果然可以，把教程贴出来为以后查看方便

## 首先安装rclone
    wget https://www.moerats.com/usr/shell/rclone_debian.sh && bash rclone_debian.sh

## 初始化配置

```
    rclone config
n) New remote
s) Set configuration password
q) Quit config
n/s/q> n
name> Rats  #随便填，后面要用到
Type of storage to configure.
Choose a number from below, or type in your own value
 1 / Amazon Drive
   \ "amazon cloud drive"
 2 / Amazon S3 (also Dreamhost, Ceph, Minio)
   \ "s3"
 3 / Backblaze B2
   \ "b2"
 4 / Box
   \ "box"
 5 / Cache a remote
   \ "cache"
 6 / Dropbox
   \ "dropbox"
 7 / Encrypt/Decrypt a remote
   \ "crypt"
 8 / FTP Connection
   \ "ftp"
 9 / Google Cloud Storage (this is not Google Drive)
   \ "google cloud storage"
10 / Google Drive
   \ "drive"
11 / Hubic
   \ "hubic"
12 / Local Disk
   \ "local"
13 / Microsoft Azure Blob Storage
   \ "azureblob"
14 / Microsoft OneDrive
   \ "onedrive"
15 / Openstack Swift (Rackspace Cloud Files, Memset Memstore, OVH)
   \ "swift"
16 / Pcloud
   \ "pcloud"
17 / QingCloud Object Storage
   \ "qingstor"
18 / SSH/SFTP Connection
   \ "sftp"
19 / Webdav
   \ "webdav"
20 / Yandex Disk
   \ "yandex"
21 / http Connection
   \ "http"
Storage> 10  #选择10，Google Drive
Google Application Client Id - leave blank normally.
client_id>  #留空 
Google Application Client Secret - leave blank normally.
client_secret>  #留空
Service Account Credentials JSON file path - needed only if you want use SA instead of interactive login.
service_account_file> 
Remote config
Use auto config?
 * Say Y if not sure
 * Say N if you are working on a remote or headless machine or Y didn't work
y) Yes
n) No
y/n> n  #选择n
If your browser doesn't open automatically go to the following link: https://accounts.google.com/o/oauth2/auth....  #复制到浏览器打开，获取验证码
Log in and authorize rclone for access
Enter verification code>  #填入上面获取到的验证码
Configure this as a team drive?
y) Yes
n) No
y/n> y  #选择y
Fetching team drive list...
No team drives found in your account--------------------
[Rats]
client_id = 
client_secret = 
service_account_file = 
token = {"access_token":"ya29.GltFBd7UJN2qrxdG8FnG_rMuB18ogb8QlujdL7glvXtfV"}
team_drive = 
--------------------
y) Yes this is OK
e) Edit this remote
d) Delete this remote
y/e/d> y  #选择y
Current remotes:
 
Name                 Type
====                 ====
Rats                 drive
 
e) Edit existing remote
n) New remote
d) Delete remote
r) Rename remote
c) Copy remote
s) Set configuration password
q) Quit config
e/n/d/r/c/s/q> q  #选择q退出

```

## 挂载硬盘（这里坑比较多）

- 首先我们要在vps上创建一个文件夹(作为Google云盘的载体盘)

    mkdir /root/GoogleDrive

- 首先我们先创建云盘文件夹

    rclone mkdir test

- 其次我们使用rclone开始挂载云盘

    rclone mount gdrive:test /root/GoogleDrive &

> gdrive是谷歌云盘标识


- 卸载文件夹
    fusermount -qzu GoogleDrive
>GoogleDrive 为你本地VPS载体文件夹

- 上传文件
    rclone copy /root/test gdrive:test

>/root/test为本地文件 后面的为谷歌云盘标识及文件夹名字

- 文件下载
    rclone copy gdrive:test /root/test

> 下载到本地vps文件夹下

- 列表

    rclone ls gdrive:test

    rclone lsl gdrive:test

> 显示上传时间
    rclone lsd gdrive:test


