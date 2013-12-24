执行脚本
=============

:该要: 在当前项目环境下执行脚本.


介绍
------------

``runscript`` 命令允许在django项目的环境下执行任意脚本.就像在 ``shell`` 命令中执行脚本一样::

  $ python manage.py shell


开始使用
---------------

首先要在项目根目录下创建一个脚本的目录,名字是 ``scripts`` ::

  $ mkdir scripts
  $ touch scripts/__init__.py

然后,创建一个想要执行的Python脚本::

  $ touch scripts/delete_all_polls.py

这个脚本文件中必须包含 ``run()`` 方法,通过 ``runscript`` 命令执行时会自动调用该方法.这个脚本中可以引用django项目中的任意模块或数据模型.

例如::

  # scripts/delete_all_polls.py

  from Polls.models import Poll

  def run():
      # Get all polls
      all_polls = Poll.objects.all()
      # Delete polls
      all_polls.delete()

提示: ``runscript`` 命令可以找到任意app下 *scripts* 目录中的脚本文件.

用法
-----

``runscript`` 命令可以在shell中调用 *scripts* 目录下的Python脚本.

例如::

  $ python manage.py runscript delete_all_polls

提示: ``runscript`` 命令会首先检查每个app下的 *scripts* 目录,如果找到对应名字的脚本就会执行.然后检查 *project_root/scripts* 目录下是否包含符合名字的脚本,如果找到也会执行.也就是说,我们可以在不同的app中创建相同名字的脚本,并且都会被执行.