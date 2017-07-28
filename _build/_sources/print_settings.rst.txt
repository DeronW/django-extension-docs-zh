print_settings
==============

:概要: ``print_settings`` 命令与Django的 ``diffsettings`` 命令相似,但是会输出当前项目中使用的全部配置(包括默认配置)

简介
------------

Django使用 ``diffsettings`` 命令输出当前项目配置与默认配置的区别.有时也需要直接查看当前项目的所有配置,尤其是配置十分复杂的时候,比如都包含好几个配置文件 [1]_.例如,在测试和开发环境中使用不同的配置文件,并且都包含了默认的 ``settings.py`` 文件,这样就不能直观的查看配置文件了.

``print_settings`` 命令支持从不同的格式文件中输出数据.

详情
---------------

最简单的输出配置命令如下,不需要添加参数::

    $ python manage.py print_settings

以不同格式输出

::

    $ python manage.py print_settings --format=json
    $ python manage.py print_settings --format=yaml    # 需要安装 PyYAML
    $ python manage.py print_settings --format=pprint
    $ python manage.py print_settings --format=text
    $ python manage.py print_settings --format=value

只显示指定参数

::

    $ python manage.py print_settings DEBUG INSTALLED_APPS
    $ python manage.py print_settings DEBUG INSTALLED_APPS --format=pprint
    $ python manage.py print_settings INSTALLED_APPS --format=value

通过 ``--help`` 参数可以获取更多帮助::

    $ python manage.py print_settings --help
    Usage: manage.py print_settings [options]

    Print the active Django settings.

    Options:
      -v VERBOSITY, --verbosity=VERBOSITY
                            Verbosity level; 0=minimal output, 1=normal output,
                            2=verbose output, 3=very verbose output
      --settings=SETTINGS   The Python path to a settings module, e.g.
                            "myproject.settings.main". If this isn't provided, the
                            DJANGO_SETTINGS_MODULE environment variable will be
                            used.
      --pythonpath=PYTHONPATH
                            A directory to add to the Python path, e.g.
                            "/home/djangoprojects/myproject".
      --traceback           Print traceback on exception
      --format=FORMAT       Specifies output format.
      --indent=INDENT       Specifies indent level for JSON and YAML
      --version             show program's version number and exit
      -h, --help            show this help message and exit

.. [1] django1.4版本后推荐配置文件全部都放在项目的 *主app* 内,到了1.6版本更进一步简化了配置文件包含的内容.但很多项目开发者会自己定义多个配置文件,以便用在不同的环境下
