# day3

## 写第一个 view

- Django 中视图的概念是「一类具有相同功能和模板的网页的集合」。比如，在一个博客应用中，你可能会创建如下几个视图：
    - 博客首页：展示最近的几项内容。
    - 内容 “详情” 页：详细展示某项内容。
    - 评论处理器：用于响应为一项内容添加评论的操作

### 最简单的 view
- 打印「hello，world」
```angular2html
article/views.py

# 导入 HttpResponse 模块
from django.http import HttpResponse

# 视图函数
def article_list(request):
    return HttpResponse("Hello World!")
```
- 有了视图函数，还需要配置 URLconfs，将用户请求的 URL 链接关联起来。

## 网站后台

Django 内置了一个很好的后台管理工具，只需要些少量代码，就可以实现强大的功能。
1. 创建管理员账号
```python manage.py createsuperuser```
2. 将 ArticlePost 注册到后台中
```
article/admin.py

from django.contrib import admin

# 别忘了导入ArticlerPost
from .models import ArticlePost

# 注册ArticlePost到admin中
admin.site.register(ArticlePost)
```
