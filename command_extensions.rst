扩展命令
==========================

:概要: 扩展命令列表

* :doc:`shell_plus` - Django shell的加强版.  自动载入所有app的models,可以方便的使用这些ORM.

* `create_app` - 新建一个app的简便方法,可以通过 --template 参数指定一个app作为模板来创建一个新的app [1]_.

* *create_command* - 在指定app内创建一个命令扩展目录,方便添加新的扩展命令(或者只能手动创建扩展命令的目录).

* *create_jobs* - 在指定app内创建一个定时任务扩展目录,可以定期执行指定任务

* *create_superuser* - 方便的创建一个超级管理员 [2]_

* *describe_form* - 显示针对一个model的form描述.复制输出的内容到forms.py中可以完整定义一个对应model的form.

* :doc:`dumpscript <dumpscript>` - Generates a Python script that will
  repopulate the database using objects. The advantage of this approach is that
  it is easy to understand, and more flexible than directly populating the
  database, or using XML.

* `export_emails`_ - 从用户表中导出联系人信息,支持多种导出格式: 地址,谷歌,Outlook,LinkedIn和VCard.

* *generate_secret_key* - 重新生成一个项目密钥.

* `graph_models`_ - 生成一个 GraphViz_ 文件.将输出内容写入一个文件.以图形化数据模型.传入多个app的名字作为参数,可以在一个文件中显示多个模型的图形化格式 [3]_.

* *mail_debug* - 开启一个邮件服务,将发出的邮件从控制台输出,而不是真的发送出去.

* *passwd* - 重新设定某个用户的密码.

* `print_settings`_ - 与 ``diffsettings`` 功能类似,但会显示Django的全部配置.

* *print_user_for_session* - 通过session key来查看当前用户信息,这个方法在查找哪个用户行为导致程序异常非常有帮助.

* *reset_db* - 重置数据库 (目前支持 sqlite3, mysql, postgres).

* *runjob* - 执行一个单独的任务, 是任务系统中的一个功能.

* *runjobs* - 执行计划任务. 分为按小时执行,按天执行,按周执行,按月执行.是任务系统中的一部分功能.

* :doc:`runprofileserver <runprofileserver>` - Starts *runserver* with hotshot/profiling tools enabled.
  I haven't had a chance to check this one out, but it looks really cool.

* `runscript`_ - 在当前项目的环境下执行脚本.

* `runserver_plus`_ - 在Werkzeug debugger模式下开启服务. 需要安装 Werkzeug_. 这是个杀手级应用.

* *set_fake_passwords* -  将所有用户的密码设置为一个统一值 (默认密码). *一定在测试环境下使用*.

* *show_urls* - 粗略的显示项目中包含的所有url.

* :doc:`sqldiff` - 显示app的models与数据库中的表的不同.这个功能非常好用,但还处于实验阶段,虽然不能捕获所有异常,但能很好的检查出不同的内容.

* :doc:`sqlcreate` - 根据配置文件的内容,生成创建数据库表的SQL语句.

* `sync_s3`_ - 将settings.MEDIA_ROOT目录中文件复制到S3中.可以通过参数设置否是使用gzip压缩,文件编码,文件的缓存时间等.

.. _`create_app`: create_app.html
.. _`export_emails`: export_emails.html
.. _`graph_models`: graph_models.html
.. _`print_settings`: print_settings.html
.. _`runscript`: runscript.html
.. _`runserver_plus`: runserver_plus.html
.. _`sync_s3`: sync_s3.html
.. _GraphViz: http://www.graphviz.org/
.. _Werkzeug: http://werkzeug.pocoo.org/

.. [1] Django1.6版本也开始支持通过模板创建app, 参考 https://docs.djangoproject.com/en/1.6/ref/django-admin/#startapp-appname-destination
.. [2] 没看到有这个命令哇 delong
.. [3] 类似MySQL的relationship map, 将models的关系以描述方式输出,虽然是文本描述,但是使用了GraphViz格式,可以打开成图形