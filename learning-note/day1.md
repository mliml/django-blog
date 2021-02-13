# day 1 

## 配置开发环境

- 安装 django（版本 V2.2）
- django 开发服务器：runserver。开发服务器会自动的检测代码的改变，并且自动加载它，因此在修改代码后不需要手动去重启服务器，非常的方便。

```python manage.py runserver```

## 创建、配置 APP

- 在 Django 中的一个 app 代表一个功能模块。开发者可以将不同功能的模块放在不同的 app 中，方便代码的复用。app 就是项目的基石，因此开发博客的第一步就是创建新的 app，用来实现跟文章相关的功能模块。
- 创建一个 APP：

```python manage.py startapp article```

```
│  db.sqlite3
│  manage.py
│
├─article
│  │  admin.py
│  │  apps.py
│  │  models.py
│  │  tests.py
│  │  views.py
│  │  __init__.py
│  │
│  └─migrations
│        └─ __init__.py
│
└─my_blog
    │  settings.py
    │  urls.py
    │  wsgi.py
    └─ __init__.py
```

- 项目结构说明
    - 根目录 my_blog 下有两个文件
      - db.sqlite3 是一个轻量级的数据库文件，用来存储项目产生的数据，比如博客文章；
      - manage.py 是项目执行命令的入口，比如 runserver
    - 目录 article 是刚创建出来的 app，用来放置博客文章相关的代码：
      - 后台管理文件 admin.py
      - 数据模型文件 models.py
      - 视图文件 views.py
      - 存放数据迁移文件的目录 migrations
    - 根目录下还有一个 my_blog 目录
      - 其中的 settings.py 包含项目的配置参数
      - urls.py 则是项目的根路由文件

# 注册 APP
- 接着我们需要修改项目配置文件，“告诉” Django 现在有 article 这么一个 app 了。

```
my_blog/settings.py

INSTALLED_APPS = [
    # 其他代码
    ...

    # 新增'article'代码，激活app
    'article',
]
```
