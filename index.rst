.. django-extensions documentation master file, created by
   sphinx-quickstart on Wed Apr  1 20:39:40 2009.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

django-extensions 文档
=============================================

Django Extensions 是针对Django框架的自定义扩展.

扩展中包括命令行的命令,扩展的数据库字段类型,后台管理扩展等.

译者注: 文档中包含了部分 `git <http://git-scm.com>`_ , `github <https://github.com/>`_ , `Python env <http://docs.python.org/2/library/os.html#os.environ>`_ 相关内容, 阅读时遇到相关只是请参考相应文档.

开始
===============

了解Django Eextensions最简单的方式是查看 `excllent screencast by Eric Holscher`__ .只要几分钟的时间,Eric就能让你了解一半的扩展命令是做什么用的.

安装
==========

可以通过pip或easy_install安装django-extensions::

    $ pip install django-extensions

或::    
    $ easy_install django-extensions

还可以从github上下载源码安装::

    $ git clone git://github.com/django-extensions/django-extensions.git
    $ cd django-extensions
    $ python setup.py install

更多安装细节,查看 :doc:`installation_instructions`.

Python和Django的版本兼容性
=================================================

django-extensions尽量根据Django版本发布计划支持相应的Django和Python版本 [1]_.

django-extensions可能在旧版本的Django或Python中运行,但是我们不会针对未支持的版本修复bug.

当前最低的Python版本要求是2.5 [2]_.

目录
========

.. toctree::
   :maxdepth: 3

   installation_instructions
   command_extensions
   command_extension_ideas
   admin_extensions
   shell_plus
   create_app
   dumpscript
   runscript
   export_emails
   field_extensions
   graph_models
   jobs_scheduling
   model_extensions
   namespace_proposal
   print_settings
   runprofileserver
   runserver_plus
   sync_s3
   sqldiff
   sqlcreate
   validate_templates


Indices and tables
==================

* :ref:`search`

__ http://ericholscher.com/blog/2008/sep/12/screencast-django-command-extensions/

.. [1] Django的某个版本指定了需要的Python版本,支持某个Django版本就代表同事支持相应的Python版本.
.. [2] 目前最新的Django1.6版本后要求不能使用Python2.6以前的版本,这也是未来Django对Python的最低要求.
