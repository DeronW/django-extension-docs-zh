create_app
============

:概要: 创建一个app的简要方法.

``--template`` 参数指定使用一个模板来创建新的app.

``--diagram`` 参数能够从 ``.dia`` 文件生成 ``models.py`` 和 ``admin.py``.

用法举例
-------------

例子需要在项目的根目录下执行,该目录下要包含 ``settings.py`` 文件 [1]_ ::

	# 获取命令行的帮助
	./manage.py create_app --help

::

	# 从 [APP_NAME].dia 文件中生成 ``models.py`` 和 ``admin.py`` ,这个文件应该放在与 ``settings.py`` 相同的文件目录下
 	./manage.py create_app -d APP_NAME

从sample.dia文件生成app
---------------------------------

::

  ./manage.py create_app --diagram=sample.dia webdata

``-d`` 参数或 ``--diagram`` 参数通过 `dia2django`_ 生成models.py, 详细文档查看 `django wiki`_.

译者注: 新版本Django原生命令 ``startapp`` 也提供了通过 ``--template`` 指定模板来创建app的功能

.. _`dia2django`: https://svn.devnull.li/main/pythonware/dia2django/trunk/doc/
.. _`django wiki`: http://code.djangoproject.com/wiki/Dia2Django

.. [1] 这个说法不准确,Django1.4版本后就独立出了配置文件目录,settings.py文件不在项目根目录下.但是这不影响使用,因为项目配置文件是通过manage.py文件指定的.