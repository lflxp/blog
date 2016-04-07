---
layout: post
title: Django web 学习
category: django
comments: true
---

# **基于Django的数据库监控系统**

```
先学习官网案例，然后把模板嵌入django框架
```

# 目录
1. 安装和环境配置[参考官网](https://docs.djangoproject.com/en/1.9/intro/install/#install-django)...................................1
2. [pip 安装](https://pip.pypa.io/en/stable/installing/#installing-with-get-pip-py)...................................2
3. 搭建[案例](https://docs.djangoproject.com/en/1.9/intro/tutorial01/)...................................3
4. [Writing your first Django app, part 1](https://docs.djangoproject.com/en/1.9/intro/tutorial01/)
5. [Writing your first Django app, part 2](https://docs.djangoproject.com/en/1.9/intro/tutorial02/)
------

> ## 安装和环境配置

# **Quick install guide**

Before you can use Django, you’ll need to get it installed. We have a [complete installation](https://docs.djangoproject.com/en/1.9/topics/install/) guide that covers all the possibilities; this guide will guide you to a simple, minimal installation that’ll work while you walk through the introduction.

## **Install Python**

Being a Python Web framework, Django requires Python. See [What Python version can I use with Django?](https://docs.djangoproject.com/en/1.9/faq/install/#faq-python-version-support) for details. Python includes a lightweight database called [SQLite](https://sqlite.org/) so you won’t need to set up a database just yet.

Get the latest version of Python at [https://www.python.org/download/](https://www.python.org/download/) or with your operating system’s package manager.

You can verify that Python is installed by typing **python** from your shell; you should see something like:

```
Python 3.4.x
[GCC 4.x] on linux
Type "help", "copyright", "credits" or "license" for more information.
```

# Writing your first Django app, part 2

## **Database setup**

Now, open up **mysite/settings.py**. It’s a normal Python module with module-level variables representing Django settings.

By default, the configuration uses SQLite. If you’re new to databases, or you’re just interested in trying Django, this is the easiest choice. SQLite is included in Python, so you won’t need to install anything else to support your database. When starting your first real project, however, you may want to use a more robust database like PostgreSQL, to avoid database-switching headaches down the road.

If you wish to use another database, install the appropriate database bindings and change the following keys in the **DATABASES 'default'** item to match your database connection settings:

- **ENGINE** – Either 'django.db.backends.sqlite3', 'django.db.backends.postgresql', 'django.db.backends.mysql', or 'django.db.backends.oracle'. Other backends are also available.
- **NAME** – The name of your database. If you’re using SQLite, the database will be a file on your computer; in that case, NAME should be the full absolute path, including filename, of that file. The default value, os.path.join(BASE_DIR, 'db.sqlite3'), will store the file in your project directory.
If you are not using SQLite as your database, additional settings such as USER, PASSWORD, and HOST must be added. For more details, see the reference documentation for DATABASES.

While you’re editing mysite/settings.py, set TIME_ZONE to your time zone.

Also, note the INSTALLED_APPS setting at the top of the file. That holds the names of all Django applications that are activated in this Django instance. Apps can be used in multiple projects, and you can package and distribute them for use by others in their projects.

By default, INSTALLED_APPS contains the following apps, all of which come with Django:

- **django.contrib.admin** – The admin site. You’ll use it shortly.
- **django.contrib.auth** – An authentication system.
- **django.contrib.contenttypes** – A framework for content types.
- **django.contrib.sessions** – A session framework.
- **django.contrib.messages** – A messaging framework.
- **django.contrib.staticfiles** – A framework for managing static files.
These applications are included by default as a convenience for the common case.

Some of these applications make use of at least one database table, though, so we need to create the tables in the database before we can use them. To do that, run the following command:

```
root@debian:/home/go/src/django_web# python manage.py migrate
Operations to perform:
  Apply all migrations: admin, contenttypes, polls, auth, sessions
Running migrations:
  Rendering model states... DONE
  Applying contenttypes.0001_initial... OK
  Applying auth.0001_initial... OK
  Applying admin.0001_initial... OK
  Applying admin.0002_logentry_remove_auto_add... OK
  Applying contenttypes.0002_remove_content_type_name... OK
  Applying auth.0002_alter_permission_name_max_length... OK
  Applying auth.0003_alter_user_email_max_length... OK
  Applying auth.0004_alter_user_username_opts... OK
  Applying auth.0005_alter_user_last_login_null... OK
  Applying auth.0006_require_contenttypes_0002... OK
  Applying auth.0007_alter_validators_add_error_messages... OK
  Applying polls.0001_initial... OK
  Applying sessions.0001_initial... OK
```


# 关键点
---


```
mysite/mysite/settings.py
DATABASES = {
    # 'default': {
    #     'ENGINE': 'django.db.backends.sqlite3',
    #     'NAME': os.path.join(BASE_DIR, 'db.sqlite3'),
    # }
     'default': {
        'ENGINE': 'django.db.backends.mysql', 
        'NAME': 'django',   
        'USER': 'root',  
        'PASSWORD': 'system', 
        'HOST': '172.16.4.51', 
        'PORT': '3306', 
    }
}
```

# 建立一个Model
---

In our simple poll app, we’ll create two models: **Question** and **Choice**. A **Question** has a question and a publication date. A **Choice** has two fields: the text of the choice and a vote tally. Each **Choice** is associated with a **Question**.

These concepts are represented by simple Python classes. Edit the **polls/models.py** file so it looks like this:

> polls/models.py

```
from django.db import models


class Question(models.Model):
    question_text = models.CharField(max_length=200)
    pub_date = models.DateTimeField('date published')


class Choice(models.Model):
    question = models.ForeignKey(Question, on_delete=models.CASCADE)
    choice_text = models.CharField(max_length=200)
    votes = models.IntegerField(default=0)
```
