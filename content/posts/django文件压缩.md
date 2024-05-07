---
title: "Django文件压缩"
date: 2019-10-11T15:28:02+08:00
draft: true
categories:
  - django
tags:
  - 文件压缩
---
<!--more-->
类型和方法数据压缩分为两种类型。

有损：在这种类型的压缩中，压缩时会降低数据质量（在这种情况下为图像和视频）。这被广泛用于压缩多媒体。

无损：在这种类型的压缩中，数据质量（在这种情况下为图像）不会丢失。它广泛用于压缩无法承受数据丢失的敏感数据。

安装与配置

安装python图像处理库 Pillow

`pip install Pillow``

我们将建立一个简单的项目来演示图像上传以及上传之前和之后的文件大小。您也可以参考Django-docs或在此处下载完整的源代码。

```python
models.py

from pil import Image
from io import BytesIO
from django.core.files.uploadedfile import InMemoryUploadedFile 
class File(models.Model):
    user = models.ForeignKey(KwsUser, verbose_name='所属用户', help_text='所属用户')
    file = models.FileField(upload_to=get_file_path, help_text='上传的文件')
    big_file = models.FileField(upload_to=get_pro_file_path, help_text='上传的原图', null=True, blank=True)
    upload_time = models.DateTimeField(auto_now_add=True, verbose_name='上传时间', null=True, blank=True)
    name = models.CharField(max_length=100, verbose_name='文件名', help_text='文件名')
    type = models.CharField(max_length=20, choices=FILETYPE, verbose_name='文件类型')
    uid = models.AutoField(primary_key=True)  # 前端数据。。。。
    minio_url = models.TextField(verbose_name='文件链接', blank=True)
    big_file_minio_url = models.TextField(verbose_name='大图文件链接', blank=True)

    def save（self，* args，** kwargs）：
        if not self.uid
            self.file = self.compressImage（ self.file
        super（File，self）.save（* args，** kwargs）
    def compressImage（self，file）：
        imageTemproary = Image.open（file）
        outputIoStream = BytesIO（）
        imageTemproaryResized = imageTemproary.resize（（1020,573））
        imageTemproary.save（outputIoStream，format ='JPEG'，quality = 60）
        outputIoStream.seek（0）
        UploadedImage = InMemoryUploadedFile（outputIoStream，'ImageField'，“％s.jpg” ％file.name.split（'.'）[0]，'image / jpeg'，sys.getsizeof（outputIoStream），None）
        return uploadImage
```

在上面的models.py文件中，我们声明名称的实用程序方法compressImage并将其uploadedImage作为参数传递。save创建Upload对象时在模块中调用此方法。

我们使用python图像处理库Pillow（PIL）来处理图像处理。我们打开上载的图像并将其存储在一个临时对象中，imageTemproary并初始化BytesIO流以处理将更改写入图像的过程。我们使用此resize()方法将上传的图像调整为特定大小（在这种情况下小于原始大小），并使用seek() method将输出流指针流重置为初始位置。我们可以进一步使用Django的InMemoryUploadedFile，以覆盖现有的未压缩的图像。
您可以继续自定义方法，以根据需要更改图像类型，尺寸和质量级别。