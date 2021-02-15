# day4

## 改写视图函数

```angular2html
article/views.py

from django.shortcuts import render

# 导入数据模型ArticlePost
from .models import ArticlePost

def article_list(request):
    # 取出所有博客文章
    articles = ArticlePost.objects.all()
    # 需要传递给模板（templates）的对象
    context = { 'articles': articles }
    # render函数：载入模板，并返回context对象
    return render(request, 'article/list.html', context)
```
- from .models import ArticlePost 从 models.py 中导入 ArticlePost 数据类
- ArticlePost.objects.all() 是数据类的方法，可以获得所有的对象（即博客文章），并传递给 articles 变量
- context 定义了需要传递给模板的上下文，这里即 articles

## 编写模板
```angular2html
templates/article/list.html

{% for article in articles %}
    <p>{{ article.title }}</p>
{% endfor %}
```
Django 通过模板来动态生成 HTML，其中就包含描述动态内容的一些特殊语法：
- {% for article in articles %}：articles 为视图函数的 context 传递过来的上下文，即所有文章的集合。{% for %} 循坏表示依次取出 articles 中的元素，命名为 article，并分别执行接下来操作。末尾用 {% endfor %} 告诉 Django 循环结束的位置。
- 使用. 符号来访问变量的属性。这里的 article 为模型中的某一条文章；我们在前面的 ArticlePost 中定义了文章的标题叫 title，因此这里可以用 article.title 来访问文章的标题。
- <p>...</p> 即为 html 语言，中间包裹了一个段落的文字。