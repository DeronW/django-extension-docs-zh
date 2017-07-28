删除优化后多余的migrations
============================

:synopsis: 把多个migrations文件优化到一个文件中, 多余的migrations文件就可以移除了

通过替换属性来实现, 移除多个migrations文件优化到一个文件后遗留的多余的migrations文件.

这个自动化过程在 `Django migration squashing
documentation`__ 中有更多描述. 这个功能会修改源码的文件结构, 小心使用. 

__ MigrationSquashingDocs_

用例
-------------

安装 *django-extensions* 后, 可以通过 *delete_squashed_migrations* 命令移除多余migrations文件. ::

  # Delete leftover migrations from the first squashed migration found in myapp
  $ ./manage.py delete_squashed_migrations myapp

  # As above but non-interactive
  $ ./manage.py --noinput delete_squashed_migrations myapp

  # Explicitly specify the squashed migration to clean up
  $ ./manage.py delete_squashed_migrations myapp 0001_squashed


.. _MigrationSquashingDocs: https://docs.djangoproject.com/en/dev/topics/migrations/#migration-squashing
