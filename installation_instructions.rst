安装django-extensions
=========================

:概要: 安装django-extensions


下载和安装
-------------------------

通过 ``pip`` 或 ``easy_install`` 安装
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

可以通过 ``pip`` 或 ``easy_install`` 安装 ``django-extensions`` ::

    $ pip install django-extensions

或::

    $ easy_install django-extensions

下载源码安装
^^^^^^^^^^^^

从 `<http://pypi.python.org/pypi/django-extensions/>`_ 下载最新的源码.解压缩后,在目录下执行Python安装命令::

    python setup.py install

...这样就可以自动安装了. 注: 这是Python默认的包安装方式.

在Django中使用
^^^^^^^^^^^^^^

在Django项目的配置文件中,把 *django_extensions* 添加到 ``INSTALLED_APPS`` 列表中::

  INSTALLED_APPS = (
      ...
      'django_extensions',
  )

这样就可以在Django的命令行中使用 ``django-extensions`` 提供的扩展命令了.

再次运行 *./manage.py help* 命令时,就可以看到新的命令.

有些新增的命令依赖其它程序或Python库,例如 [1]_

* 'export_emails' 需要 *python vobject* 模块来创建vcard文件

* 'graph_models' 需要 *pygraphviz* 库来渲染图片文件.

如果执行的django-extensions命令依赖的程序或库没有安装(或不在当前的环境中),那么这条命令被执行时会抛出异常,并提示缺少的依赖程序或库.

版本控制
---------------

``django-extensions`` 目前被托管在github上: `<https://github.com/django-extensions/django-extensions>`_

*django command extensions* 的dev版本在包含了新特性的同时还可以稳定运行,在正式环境下也推荐使用 [2]_. 

使用git命令克隆 ``django-extensions`` 源码到本地::

  git clone git://github.com/django-extensions/django-extensions.git

下载源码后可以在项目根目录下执行 ``python setup.py install`` 安装,或将 *extensions* 目录添加到Python环境变量中.最通用的做法是创建一个软连接指向代码的目录,并将软连接添加到Python环境变量中.比如Python的site-packages目录 [3]_::

  ln -sf /full/path/to/django-extensions/django_extensions /usr/lib/python2.7/site-packages/django_extensions

检查django-extensions是否被正确安装,在Python的shell中输入下面命令 [4]_::

  >>> import django_extensions
  >>> django_extensions.VERSION
  (1, 2, 5)

注意:通过git克隆出来的代码比通过源包(pypi)安装的代码版本更新.通过源码安装虽然可能会包含bug或兼容性问题,但也会包含一些新特性.


.. [1] vcard是电子名片的格式
.. [2] 在线上的服务中同样可以使用dev版的command extensions,不过通过pip安装时只会安装stable版本,如果要用dev就要手动安装.注意: 这里推荐的是 *command extensions* ,而不是 django-extensions
.. [3] Python的环境变量可以在多个地方,译者不认为建立代码目录软连接到系统环境变量的方式不够优美,推荐使用pip安装
.. [4] 或在shell中执行 python -c 'import django_extensions;print django_extensions.VERSION'