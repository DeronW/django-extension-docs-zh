sqldiff
=======

:概要: ``sqldiff`` 命令输出指定app的表结构修改语句.

``sqldiff`` 命令扫描指定app的数据模型,并与数据库中的表结构进行比较,输出差别.

``sqldiff`` 命令不是用来合并数据库差别的工具,虽然能够查看区别,但这个命令的设计初衷只是检查数据库表结构与django数据模型的区别.

支持的数据库
-------------------

``sqldiff`` 命令当前支持的数据库:

* PostgreSQL
* Sqlite3
* MySQL
* Oracle

欢迎提供支持其它数据库的patch! :-)

用法举例
-------------

::

	# 查看所有app数据模型与数据库之间的区别
 	$ ./manage.py sqldiff -a

::

  	# 用文本显示所有app数据模型与数据库之间的区别
	$ ./manage.py sqldiff -a -t
