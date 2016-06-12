sqldsn
========

:概要: 在标准输出中打印数据资源的名称和关系.


支持的数据库
-------------------

目前仅支持下面的数据库:

* PostgreSQL (psycopg2 or postgis)
* Sqlite3
* MySQL

欢迎贡献代码, 支持更多的数据库! :-)

退出状态码
----------

退出状态码始终是 0


用法举例
-------------

::

  # 打印默认数据库资源名称
  $ ./manage.py sqldsn

::

  # 打印所有数据库资源名称
  $ ./manage.py sqldsn --all

::

  # 打印 'slave' 数据库的资源名称
  $ ./manage.py sqldsn --router=slave

::
0
  # 打印默认数据库所有可用资源
  $ ./manage.py sqldsn --style=all

::

  # 使用 quite(安静) 模式, 通过默认数据库生成 .pgpass 文件
  $ ./manage.py sqldsn -q --style=pgpass > .pgpass