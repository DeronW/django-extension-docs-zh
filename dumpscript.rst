dumpscript
==========

:概要: 生成单独的Python脚本,包含指定app对应的数据库数据对象.可以用来将数据表导入数据库.

``dumpscript`` 命令生成单独的Python脚本,包含了转换成Python对象的数据库数据.这种方法比直接创建数据库或通过XML创建数据库更容易理解,扩展性也更好.

为什么有这个功能
----------------

这样做的有几点好处:

* 数据库变更时会少出现些莫名其妙的错误: 不依赖ID的外键,会忽略掉新增和删除的列

* 编辑脚本后可以自动生成很多的实例数据

例如,编辑一个脚本,生成一些测试的初始数据到数据库中::

  for i in xrange(2000):
      poll = Poll()
      poll.question = "Question #%d" % i
      poll.pub_date = date(2001,01,01) + timedelta(days=i)
      poll.save()

真实情况下数据库可能更大更复杂,通常是通过Admin后台生成一下测试数据,再导出脚本.编辑导出的脚本,得到更多的数据.

特性支持
--------

* 外键和多对多关系(通过Python变量,而不是ID)
* 外键或多对多中对自己的引用
* models子类
* *ContentType* 字段类型, 并生成关联关系
* 递归引用
* 排除自增字段
* 父类不会被包含,除非没有子类继承它
* 可以引用单独的类

如何使用
------------

从指定的app中导出所有models的建表语句::

  $ ./manage.py dumpscript appname > scripts/testdata.py

导出指定模型的数据,添加参数 ``appname.ModelName`` ::

  $ ./manage.py dumpscript appname.ModelName > scripts/testdata.py

清空指定app对应数据库数据,然后重新加载数据::

  $ ./manage.py reset appname
  $ ./manage.py runscript testdata

提示: ``runscript`` 命令只能执行在 ``scripts`` 模块下的脚本,所以要在 ``scripts`` 目录下创建 *__init__.py* 文件.

警告
-------

命名冲突
~~~~~~~~~~~~~~~~

在命名输出文件时不要与当前环境路径下的文件重名,否则会引起import异常.比如输出到的目标文件与app目录重名时,脚本会尝试加载输出文件而不是app,这是不正确的.

例子::

  # 错误用法
  $ ./manage.py dumpscript appname > dumps/appname.py

  # 正确用法
  $ ./manage.py dumpscript appname > dumps/appname_all.py

  # 正确用法
  $ ./manage.py dumpscript appname.Somemodel > dumps/appname_somemodel.py
