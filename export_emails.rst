export_emails
=============

:概要: 以不同的格式导出用户的邮件列表

大部分Django站点包含注册用户的信息.有时我们需要将用户邮箱信息导入到其它系统中(生成邮件, GMail, google docs, 修改权限, LinkedLn用户组等等). ``export_emails`` 命令为此而设计.导出的用户信息的同时可以对其进行分组.

用法举例
-------------

将所有用户信息导出成 ``'"First Last" <my@addr.com>;'`` 格式::

  $ ./manage.py export_emails > addresses.txt

以LinkedIn pre-approve格式从 ``Attendees`` 组中导出用户信息::

  $ ./manage.py export_emails -g Attendees -f linkedin pycon08.csv

以GMail(Google Docs)格式创建一个CSV文件::

 	$ ./manage.py export_emails --format=google google.csv

可选用的格式
-------------------------

address
^^^^^^^

默认的文本格式,每个实例占一行并保存成如下格式::

  "First Last" <user@host.com>;

这可以被用在任意的邮件服务中.

google
^^^^^^

CSV格式文件,可以导入到google的应用中.可以被直接用在GMail中,在GMail中添加一组邮件列表,谷歌文档的邀请,谷歌文档权限批量修改,谷歌日历服务,等等.

输出文件仅包含两列.一列是用户名,一列是邮箱地址.这个格式也适合用来做电子表格文件.

outlook
^^^^^^^

CSV格式文件,可以导入到到Outlook,支持Outlook中的'必填'字段,但只有name和email有值.


linkedin
^^^^^^^^

CSV格式文件,可以被导入到 `LinkedIn Groups`_ ,邀请列表中的用户加入该组.

包含3列数据: ``名`` ``姓`` ``邮箱`` .这也是最适合电子表格的格式.

vcard
^^^^^

vCard格式,可以被导入到苹果系统的联系人目录中.

.. _`LinkedIn Groups`: http://www.linkedin.com/static?key=groups_info
