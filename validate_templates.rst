validate_templates
=======================

:概要: 检查模板的语法错误或编译错误.

参数
-------

verbosity
~~~~~~~~~

该参数表示使用高级输出错误信息详细级别,会将所有检查过的模板的错误全部输出.否则只会输出最近的查找到错误的文件信息.

break
~~~~~

遇到错误就直接输出不再继续检查

includes
~~~~~~~~

通过参数 ``-i`` (可以重复使用)来添加自定义的模板目录

配置
--------

VALIDATE_TEMPLATES_EXTRA_TEMPLATE_DIRS
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

通过 ``VALIDATE_TEMPLATES_EXTRA_TEMPLATE_DIRS`` 配置可以指定所有模板目录的前缀.这个配置主要针对 ``TEMPLATE_DIRS`` 是动态的或模板目录是通过中间件生成的情况.扩展app的模板,比如Django项目中若是包含的 ``celery`` 模块也可以通过指定该参数来进行模板语法检测.

用法举例
-------------

::

	./manage.py validate_templates

译者注: ``validate_templates`` 命令适用与检测Django框架原生模板,如果使用了其它模板(jinja等),则该命令会失去检测效果.