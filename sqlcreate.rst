sqlcreate
=============

:概要: ``sqlcreate`` 命令可以更方便的创建数据库.


简介
-------------

不用再手动创建数据库, ``settings.py`` 文件中已经包含了需要的信息,所以Do It Yourself.

用法
-------------

::

  $ python manage.py sqlcreate [--router=<routername>] | <my_database_shell_command>
  
``sqlcreate`` 命令会将SQL语句输出用来检查(如果你想检查的话).但最终还是要输入到数据库的shell中来执行.

如果有合适的方法证明当前用户有修改数据库的权限,那就可以把输出结果直接导入到数据库中.但是因为项目的配置方式,这种直接修改数据库的方式是不能接受的.

例子
-------------

PostgreSQL
~~~~~~~~~~

::

  $ ./manage.py sqlcreate [--router=<routername>] | psql -U <db_administrator> -W
  

MySQL
~~~~~

::

  $ ./manage.py sqlcreate [--router=<routername>] | mysql -u <db_administrator> -p
  

存在的问题
------------

* CREATE DATABASE 不是SQL标准语句,所以可能不能支持所有数据库 [1]_.

* 回滚数据库时没有创建用户名及密码,但缺尝试分配一个数据库用户 [2]_ .

* 缺少表空间的设置,等等.

.. [1] sqlite3 数据库创建就不是通过CREATE DATABASE语句,不过绝大多数数据库都没问题.
.. [2] 译者也不确定明白这个问题指的是什么.sorry.