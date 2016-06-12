shell_plus
==========

:概要: shell命令的扩展命令,运行Django shell的同时自动加载所有app的models,并选择使用Python shell的版本.

交互式的 Python Shells
-------------------------

shell_plus支持3种交互的Python shell.

BPython::

  $ ./manage.py shell_plus --bpython

IPython::

  $ ./manage.py shell_plus --ipython

Python::

  $ ./manage.py shell_plus --plain


默认shell优先顺序是: bpython, ipython, python.

也可以在 ``settings.py`` 配置中指定优先选择的shell工具::

  # 在shell_plus中使用ipython作为交互工具
  SHELL_PLUS = "ipython"

配置
-------------

如果遇到apps中包含的的models名字出现冲突,或不想载入特定apps的models的情况,可以通过配置别名的方法解决:

提示: 下列配置仅在shell_plus中生效,不会影响当前项目运行的环境变量

::

  # 将自动载入的Messages模块重命名为blog_messages

  SHELL_PLUS_MODEL_ALIASES = {'blog': {'Messages': 'blog_messages'},}

::

  # 自动载入的 myblog 模型添加前缀
  SHELL_PLUS_APP_PREFIXES = {'blog': 'myblog',}

::

  # 不加载sites app和pictures的blog模型

  SHELL_PLUS_DONT_LOAD = ['sites', 'blog.pictures']

设置别名和声明不加载的配置可以同时使用.也可以通过命令行参数设置不加载的模块::

  $ ./manage.py shell_plus --dont-load app1 --dont-load app2.module1

命令行的参数和配置文件中的设置是可以同时使用的,所以一次性的参数完全可以通过命令行运行,省去频繁修改配置文件的麻烦.

shell_plus还能使用 `IPython Notebook`_ .将浏览器作为交互的shell::

    $ ./manage.py shell_plus --notebook

通过修改2个参数可以自定义 IPython 的行为.

第一个是 ``NOTEBOOK_ARGUMENTS`` , 可以追加自定义参数, 需要通过下面方式启动::

    $ ipython notebook -h

例如::

    NOTEBOOK_ARGUMENTS = [
        '--ip=x.x.x.x',
        '--port=xx',
    ]

另一个参数是  ``IPYTHON_ARGUMENTS`` ,通过下面方式启动::

    $ ipython -h

``IPython Notebook`` 中也会将所有模块和models加载到全局变量中.

``IPython NoteBook`` 中自动加载模块功能是通过参数配置的,默认为启用状态.::

  --ext django_extensions.management.notebook_extension

自定义 ``IPython Notebook`` 配置需要覆盖Django项目的 ``IPYTHON_ARGUMENTS`` 配置::

    IPYTHON_ARGUMENTS = [
        '--ext', 'django_extensions.management.notebook_extension',
        '--ext', 'myproject.notebook_extension',
        '--debug',
    ]

想在 ``IPython Notebook`` 中启用自动加载功能,要么包含django-extensions默认的notebook扩展配置,要么把自动加载的代码拷贝到自定义的扩展中.

提示: ``IPython Notebook`` 的特性中不能识别 ``--dont-load`` 参数.

附加的引入模块
------------------

在配置文件中设置 ``SHELL_PLUS_PRE_IMPORTS`` 和 ``SHELL_PLUS_POST_IMPORTS`` 可以指定附加的引入模块.第一个配置中添加的模块会先于所有模块加载,第二个配置中添加的模块会后于所有模块加载.这两个配置的格式相同,在settings.py文件中添加::

    SHELL_PLUS_PRE_IMPORTS = (
        ('module.submodule1', ('class1', 'function2')),
        ('module.submodule2', 'function3'),
        ('module.submodule3', '*'),
        'module.submodule4'
    )

上面的配置被转换为Python的引入代码结果,如下所示::

    from module.submodule1 import class1, function2
    from module.submodule2 import function3
    from module.submodule3 import *
    import module.submodule4

这些引入的变量在shell执行时就可以使用了.

数据库应用签名
-------------

使用PostgreSQL ``application_name`` 默认被设置为 ``django_shell`` , 这样能够区分 shell_plus 下的查询语句.


.. _`IPython Notebook`: http://ipython.org/ipython-doc/dev/interactive/htmlnotebook.html
