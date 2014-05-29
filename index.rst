
django-extensions 文档
=============================================

Django Extensions 是Django框架的扩展功能集合.

包括management命令扩展,数据库字段扩展,admin后台扩展等.

译者注: 文档中包含了部分 `git <http://git-scm.com>`_ , `github <https://github.com/>`_ , `Python env <http://docs.python.org/2/library/os.html#os.environ>`_ 相关内容, 阅读时遇到相关只是请参考相应文档.

开始
======

了解Django Eextensions最简单的方式是查看 `excllent screencast by Eric Holscher`__ .只要几分钟的时间,Eric就能让你了解一半的扩展命令是做什么用的.

安装
======

通过 ``pip`` 或 ``easy_install`` 安装 ``django-extensions``::

    $ pip install django-extensions

或::

    $ easy_install django-extensions

还可以从github上下载源码安装::

    $ git clone git://github.com/django-extensions/django-extensions.git
    $ cd django-extensions
    $ python setup.py install

更多安装细节,查看 :doc:`installation_instructions`.

兼容性
=======

``django-extensions`` 尽量根据Django版本发布计划支持相应的Django和Python版本 参考Django版本支持说明_ [1]_ .

新版本的 ``django-extensions`` 可能在旧版本的Django或Python中也会正常运行,但是我们已经放弃修复与旧版本Django或Python的兼容性bug.

目前支持的Python版本是 2.6, 2.7 和 3.3， 支持的Django版本是1.4, 1.5, 1.6 [2]_.

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

__ http://ericholscher.com/blog/2008/sep/12/screencast-django-command-extensions/
.. _参考Django版本支持说明: https://docs.djangoproject.com/en/dev/internals/release-process/#supported-versions

.. [1] Django的单个版本指定了需要的Python版本,支持某个Django版本就代表同时支持相应的Python版本.
.. [2] 目前最新的Django1.6版本后要求不能使用Python2.6以前的版本,这也是未来Django对Python的最低要求.应及时升级Django到最新的稳定版,以免欠下技术债.
