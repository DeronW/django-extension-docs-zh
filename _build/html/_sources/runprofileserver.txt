runprofileserver
================

*首先,在跟踪\分析一门语言和框架前,应该深入了解一下正在使用的语言(框架),这样才能事半功倍.不够扎实的功底会导致在跟踪分析服务时做出错误的假设和判断.有一条经验法则很实用:干净整洁的代码比热情和耐心更实用.*

*这部分功能正在持续改进中,如果你有好的办法能够跟踪,分析Django框架,请给我们留言*

简介
------------

``runprofileserver`` 命令在启动django服务的同时其用了跟踪分析工具,会将服务的分析信息保存到 ``.prof`` 后缀文件中.使用 ``--prof-path`` 参数指定保存分析文件到指定目录.每一个请求的分析数据都会被保存成一个profile文件.

如果没有指定 ``--prof-path`` 参数,分析数据的 ``.prof`` 文件会被保存到 ``/tmp`` 目录下.建议使用特定目录保存分析文件,这样方便我们随时查看分析数据,也不会弄乱 ``/tmp`` 目录,使用windows系统时一定要指定``--prof-path`` 参数,因为windows系统没有 ``/tmp`` 目录.

分析文件的名字默认名字是::

  {path}.{duration:06d}ms.{time}

也可以通过 ``--prof-file`` 参数指定生成的服务分析文件名字.文件名格式规则参考: `Format Specification <http://docs.python.org/3/library/string.html#formatspec>`_.


例如:

  * "{time}-{path}-{duration}ms" - 用请求的道达时间命名分析文件.
  * "{duration:06d}ms.{path}.{time}" - 用请求的相应时间命名分析文件.

聚合profile
-----------------------

Django提供了一个profile文件聚合的工具 ``gather_profile_stats.py`` ,在Django安装目录的 ``bin`` 目录下可以找到.

Profiler选择
-------------

``runprofileserver`` 支持两种 profilers : *hotshot* 和 *cProfile*. 两个都是Python标准库. *cProfile* 比较新, 而且可能不支持所有系统. 所以默认的 profiler 是*hotshot*.

但是 *hotshot* 已经不再维护了. <https://docs.python.org/2/library/profile.html#introduction-to-the-profilers>`_
*cProfile* 通常是一个更好的选择. 通过 ``--use-cprofile`` 参数来检测当前系统是否支持 *cProfile*;

例子::

  $ mkdir /tmp/my-profile-data
  $ ./manage.py runprofileserver --use-cprofile --prof-path=/tmp/my-profile-data

如果使用默认profiler后, ``pstats`` 模块和 GUI 工具都打不开记录, 并且提示 "*ValueError: bad marshal data (unknown type code)*". 尝试使用*cProfile*作为profiler来解决问题.

KCacheGrind
-----------

新版本的 ``runprofileserver`` 命令可以把分析的结果文件保存成 `KCacheGrind`_ 格式文件,这样就可以通过 KCacheGrind 的分析工具来查看分析数据.

例子::

  $ mkdir /tmp/my-profile-data
  $ ./manage.py runprofileserver --kcachegrind --prof-path=/tmp/my-profile-data
  Validating models...
  0 errors found

  Django version 1.0-post-release-SVN-SVN-unknown, using settings 'complete_project.settings'
  Development server is running at http://127.0.0.1:8000/
  Quit the server with CONTROL-C.
  [13/Nov/2008 06:29:38] "GET / HTTP/1.1" 200 41107
  [13/Nov/2008 06:29:39] "GET /site_media/base.css?743 HTTP/1.1" 200 17227
  [13/Nov/2008 06:29:39] "GET /site_media/logo.png HTTP/1.1" 200 3474
  [13/Nov/2008 06:29:39] "GET /site_media/jquery.js HTTP/1.1" 200 31033
  [13/Nov/2008 06:29:39] "GET /site_media/heading.png HTTP/1.1" 200 247
  [13/Nov/2008 06:29:39] "GET /site_media/base.js HTTP/1.1" 200 751
  <ctrl-c>
  $ kcachegrind /tmp/my-profile-data/root.12574391.592.prof

.. images: http://trbs.net/media/misc/django-runprofileserver-kcachegrind-full.jpg

相关知识链接
----------------

* http://code.djangoproject.com/wiki/ProfilingDjango
* http://www.rkblog.rk.edu.pl/w/p/django-profiling-hotshot-and-kcachegrind/
* http://code.djangoproject.com/browser/django/trunk/django/bin/profiling/gather_profile_stats.py
* http://www.oluyede.org/blog/2007/03/07/profiling-django/
* http://simonwillison.net/2008/May/22/debugging/

.. _KCacheGrind: http://kcachegrind.sourceforge.net/html/Documentation.html
