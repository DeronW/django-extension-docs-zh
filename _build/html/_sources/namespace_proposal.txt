命名空间的建议
==================

:概要: 命名空间的建议


简介
------------

Please change / write your proposal for splitting django_extensions into
namespaces here.
请使用 ``django_extensions`` 的命名空间,而不是绝对路径


命名空间的建议
-----------------------

一些简单的建议:

* django_extensions.commands (20% 的人在正式环境中使用路径)

* django_extensions.commands.development (所有在开发中用到的功能)

* django_extensions.commands.extra

* django_extensions.db

* django_extensions.templates

* django_extensions.jobs

数据库部分使用方式都是正确的,因为目前只有一种引用方式::

  from django_extensions.db.models import something