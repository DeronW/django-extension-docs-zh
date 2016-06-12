数据库字段扩展
================

:概要: 数据字段的扩展


数据库字段的扩展
----------------

* ``TimeStampedModel`` - 抽象类,包含了由自己管理的 ``created`` 和 ``modified`` 字段.
* ``TitleDescriptionModel`` - 虚拟类, 包含了title和description两个字段.
* ``TitleSlugDescriptionModel`` - 虚拟类, 包含了title和description两个字段. 并具有自动管理 slug 字段的功能. slug字段生成字title字段.