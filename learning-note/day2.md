# day 2

## 编写博客文章的 Model 模型

- 编写 Model.py
```
article/models.py

from django.db import models
# 导入内建的User模型。
from django.contrib.auth.models import User
# timezone 用于处理时间相关事务。
from django.utils import timezone

# 博客文章数据模型
class ArticlePost(models.Model):
    # 文章作者。参数 on_delete 用于指定数据删除的方式
    author = models.ForeignKey(User, on_delete=models.CASCADE)

    # 文章标题。models.CharField 为字符串字段，用于保存较短的字符串，比如标题
    title = models.CharField(max_length=100)

    # 文章正文。保存大量文本使用 TextField
    body = models.TextField()

    # 文章创建时间。参数 default=timezone.now 指定其在创建数据时将默认写入当前的时间
    created = models.DateTimeField(default=timezone.now)

    # 文章更新时间。参数 auto_now=True 指定每次数据更新时自动写入当前时间
    updated = models.DateTimeField(auto_now=True)
```
- 每个模型都被表示为 django.db.models.Model 类的子类，从它继承了操作数据库需要的所有方法。
- 每个字段都是 Field 类的实例 。比如字符字段被表示为 CharField ，日期时间字段被表示为 DateTimeField。这将告诉 Django 要处理的数据类型。
- 定义某些 Field 类实例需要参数。例如 CharField 需要一个 max_length 参数。这个参数的用处不止于用来定义数据库结构，也用于验证数据。
- 使用 ForeignKey 定义一个关系。这将告诉 Django，每个（或多个） ArticlePost 对象都关联到一个 User 对象。
---
- 我们还可以额外再定义一些内容，规范 ArticlePost 中数据的行为：
```angular2html
article/models.py

...

class ArticlePost(models.Model):
    ...

    # 内部类 class Meta 用于给 model 定义元数据
    class Meta:
        # ordering 指定模型返回的数据的排列顺序
        # '-created' 表明数据应该以倒序排列
        ordering = ('-created',)

    # 函数 __str__ 定义当调用对象的 str() 方法时的返回值内容
    def __str__(self):
        # return self.title 将文章标题返回
        return self.title
```

## 数据迁移
- 每当对数据库进行了更改（添加、修改、删除等）操作，都需要进行数据迁移。
```angular2html
python manage.py makemigrations

python manage.py migrate
```