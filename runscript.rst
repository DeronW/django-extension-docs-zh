runscript
=============

:该要: 在当前项目环境下执行脚本,这个功能非常有用,它能够允许在不启动Django服务的同时以Django项目的环境变量执行脚本方法.

介绍
------------

``runscript`` 命令允许在django项目的环境下执行任意脚本.就像在 ``shell`` 命令中执行脚本一样::

  $ python manage.py shell

开始使用
---------------

这个例子假设你跟着 Django1.8+ 版本的入门教程, 创建了 polls app,并包含``Question``模型. 我们将创建一个脚本, 从数据库中删除所有``Question``的数据.

首先要在项目根目录下创建一个脚本的目录,名字是 ``scripts`` ::

  $ mkdir scripts
  $ touch scripts/__init__.py

然后,创建一个想要执行的Python脚本::

  $ touch scripts/delete_all_questions.py

这个脚本文件中必须包含 ``run()`` 方法, ``runscript`` 命令执行时会自动调用该方法.这个脚本中可以引用django项目中的任意模块或数据模型.

例如::

  # scripts/delete_all_questions.py

  from polls.models import Question

  def run():
      # Fetch all questions
      questions = Question.objects.all()
      # Delete questions
      questions.delete()

提示: ``runscript`` 命令可以找到任意app下 *scripts* 目录中的脚本文件.

用法
-----

``runscript`` 命令可以在shell中调用 *scripts* 目录下的Python脚本.

例如::

  $ python manage.py runscript delete_all_questions

提示: ``runscript`` 命令会首先检查每个app下的 *scripts* 目录,如果找到对应名字的脚本就会执行.然后检查 *project_root/scripts* 目录下是否包含符合名字的脚本,如果找到也会执行.也就是说,我们可以在不同的app中创建相同名字的脚本,并且都会被执行.

参数
----

``--script-args`` 参数可以接收逗号分隔的值，并将其作为参数传递到方法内，例如

::

    $ python manage.py runscript delete_all_questions --script-args=staleonly

例子中 ``--script-args`` 参数值作为执行脚本的 *run()* 方法的参数传入，使用举例

::

  # scripts/delete_all_questions.py
  from datetime import timedelta

  from django.utils import timezone

  from polls.models import Question

  def run(*args):
      # Get all questions
      questions = Question.objects.all()
      if 'staleonly' in args:
          # Only get questions more than 100 days old
          questions = all_questions.filter(pub_date__lt=timezone.now() - timedelta(days=100))
      # Delete questions
      questions.delete()
