management 命令扩展
===================

:概要: management扩展命令列表

* :doc:`shell_plus` - Django shell的加强版. 自动载入所有app的models,可以方便的使用这些ORM.

* ``admin_generator`` - 提供app名字后, 自动生成Admin类. 生成的代码会输出到标准输出中(STDOUT).

* :doc:`create_app` - 新建一个app的简便方法,可以通过 ``--template`` 参数指定一个app作为创建模板 [1]_.

* ``create_command`` - 在指定app内创建一个命令扩展目录,方便添加新的扩展命令(或者只能手动创建扩展命令的目录).

* ``create_template_tags`` - 在制定的app内创建模板标签目录

* ``create_jobs`` - 在指定app内创建一个定时任务扩展目录,可以定期执行指定任务.

* ``create_superuser`` - 方便的创建一个超级管理员 [2]_.

* ``clear_cache`` - 清楚缓存, 在测试和部署过程中十分有用.

* ``describe_form`` - 显示针对一个model的form描述.复制输出的内容到forms.py中可以完整定义一个对应model的form.

* :doc:`dumpscript` - 生成一个Python脚本.包含指定app的所有数据对象.与Django的 ``dumpdata`` 命令不同的是 ``dumpscript`` 导出的是Python对象,而不是纯数据.这种导出数据的方式比直接导出数据或XML文件更容易理解,也更灵活.

* :doc:`export_emails` - 从用户表中导出联系人信息,支持多种导出格式: 地址,谷歌,Outlook,LinkedIn和VCard.

* ``generate_secret_key`` - 重新生成一个项目密钥, ``settigns.py`` 文件中的 **SECRET_KEY** 配置.

* :doc:`graph_models` - 生成一个 GraphViz_ 文件.将输出内容写入一个文件.以图形化数据模型.传入多个app的名字作为参数,可以在一个文件中显示多个模型的图形化格式 [3]_.

* ``mail_debug`` - 开启一个邮件服务,将Django项目发出的邮件从控制台输出,而不是真的发送出去.

* ``passwd`` - 重新设定某个用户的密码,用法: *./manage.py passwd [用户名]* .

* ``pipchecker`` - 扫描pip依赖文件 [3]_ 并找出需要更新的包. 类似于 ``pip list -o`` 命令安装依赖包的过程(在虚拟环境中 virtualenv), 只不过它是通过pip依赖文件实现的.

* :doc:`print_settings` - 与 ``diffsettings`` 命令功能类似,但会根据参数显示指定的配置，如果不传参数默认显示的全部配置.

* ``print_user_for_session`` - 通过 ``session key`` 来查看当前用户信息,这个方法在查找哪个用户行为导致程序异常非常有帮助. 仅在``SESSION_ENGINE``设置为``'django.contrib.sessions.backends.db'``(默认值)的时候才能正常工作

* ``drop_test_database`` - 删除测试数据库. 在自动化测试/部署系统(BuildBot, Jenkins, 等等)中十分有用. 确保测试数据库最终会被清除掉.

* ``reset_db`` - 重置数据库 (目前支持 sqlite3, mysql, postgres)，可以用来删除或创建数据库.

* ``runjob`` - 执行一个单独的任务,是 ``django-extensions`` 任务系统中的一个功能.

* ``runjobs`` - 按计划定期执行任务. 按 小时,天,周,月执行. 时间计划功能是系统任务的一部分.

* ``runjobs`` - 执行计划任务. 分为按小时执行,按天执行,按周执行,按月执行.是 ``django-extensions`` 任务系统中的一部分功能.

* :doc:`runprofileserver` - 在启动 ``runserver`` 测试服务的同时,其用 ``profile`` 功能,可以记录服务的详细日志,包含了对于Python方法的详细执行分析.在服务器性能分析时,这是最佳方法了.

* :doc:`runscript` - 在当前项目的环境下执行脚本.

* :doc:`runserver_plus` - 在Werkzeug debugger模式下开启服务. 需要安装 Werkzeug_.这是个杀手级应用.

* ``set_fake_passwords`` -  将所有用户的密码设置为一个统一值 (默认密码). *一定要在测试环境下使用*.

* ``show_urls`` - 统一显示项目中包含的所有url.

* :doc:`sqldiff` - 显示app的models与数据库中的表的差别.这个功能非常好用,但还处于实验阶段,虽然不能捕获所有异常,但能很好的检查出不同的内容 [4]_.

* :doc:`sqlcreate` - 根据配置文件的内容,生成创建数据库表的SQL语句.

* :doc:`sqldsn` - 从Django的配置文件中读取数据库连接参数. 可以提供给其它系统使用.

* :doc:`sync_s3` - 将settings.MEDIA_ROOT目录中文件复制到S3中.可以通过参数设置否是使用gzip压缩,文件编码,文件的缓存时间等.

.. _GraphViz: http://www.graphviz.org/
.. _Werkzeug: http://werkzeug.pocoo.org/

.. [1] Django1.6版本也开始支持通过模板创建app, 参考 https://docs.djangoproject.com/en/1.6/ref/django-admin/#startapp-appname-destination
.. [2] 没看到命令列表里有这个命令哇!!!
.. [3] 类似MySQL的relationship map, 将models的关系以描述方式输出,虽然是文本描述,但是使用了GraphViz格式,可以打开成图形
.. [4] 目前Django项目中数据库表管理基本都使用Python的South库,跟Django可以很好的正好到一起,管理数据库也十分方便.
.. [5] 一般是项目根目录下的requirements.txt