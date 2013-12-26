定时任务
===============

:概要: 在Django-extensions中使用定时任务.

定时的计划任务
--------------

本页介绍的功能正在努力改进中
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

新建一个与Django的命令执行方式类似的任务 [1]_.使用 ``create_jobs`` 命令在一个app内创建一个 'jobs' 目录,然后可以创建不同的Python脚本执行不同的任务.

``django_extensions.jobs`` 目录中包含了一些简单的例子.

Python的任务脚本继承定时任务类后就会被定义为任务,可以按小时,按天,按周或按月执行.继承的脚本必须实现 ``execute`` 方法,该方法在任务触发时会被自动执行.

与任务相关的命令还包括:

* create_jobs: 创建包含任务的目录

* runjob: 执行单独的任务

* runjobs: 执行所有任务

列出所有任务::

	runjob[s] -l

未触发时,任务不会自己执行.

任务需要手动执行,或指定时间执行,或在 ``cron`` 中配置定期执行::

	@hourly /path/to/my/project/manage.py runjobs hourly

	@daily /path/to/my/project/manage.py runjobs daily

	@weekly /path/to/my/project/manage.py runjobs weekly

	@monthly /path/to/my/project/manage.py runjobs monthly

.. [1] 意味着可以想Django的shell命令那样引入项目中的app相关类和方法