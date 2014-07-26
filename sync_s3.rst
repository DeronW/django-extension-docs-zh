sync_s3
==============

:概要: 将项目的 ``MEDIA_ROOT`` 和 ``STATIC_ROOT`` 目录包含的文件同步到S3 [1]_.

``sync_s3`` 命令会检索配置中的 ``settings.MEDIA_ROOT`` 目录和 ``settings.STATIC_ROOT`` 目录,然后把所有文件资源上传到S3的相同的目录结构下.

``sync_s3`` 命令可以启用以下功能,通过传入参数启用对应功能,默认全部关闭::

  * gzip 压缩CSS和JS文件,并添加 ``Content-Encoding`` 头.
  * 设置文件缓存过期时间
  * 只上传 media 或 static 目录文件.
  * 使用其它的S3同步工具
  * 设置public文件的访问控制列表

用法举例
-------------

上传到S3的 mybucket ::

  $ ./manage.py sync_s3 mybucket

上传到S3的 mybucket ,并对CSS/JS文件进行gzip压缩和添加缓存过期时间::

  $ ./manage.py sync_s3 mybucket --gzip --expires

只上传 media 文件到S3的 mybucket 中

::

    $ ./manage.py sync_s3 mybucket  --media-only  # or --static-only

::

    # Upload only media files to a S3 compatible provider into the bucket 'mybucket' and set private file ACLs
    $ ./manage.py sync_s3 mybucket  --media-only  --s3host=cs.example.com --acl=private

依赖的库和配置
-------------------------------

``sync_s3`` 命令需要安装 ``boto`` 库,改命令在1.4c版本下测试通过:

  http://code.google.com/p/boto/

当然还要添加AWS账户的S3密钥和bucket名称,在项目配置文件 ``settings.py`` 文件中增加配置::

  # settings.py
  AWS_ACCESS_KEY_ID = ''
  AWS_SECRET_ACCESS_KEY = ''
  AWS_BUCKET_NAME = 'bucket'


可选配置
---------

可以在 ``settings.py`` 文件种设置好全部的 ``sync_s3`` 的参数，实现自动上传

::

    # settings.py
    AWS_S3_HOST = 'cs.example.com'
    AWS_DEFAULT_ACL = 'private'
    SYNC_S3_PREFIX = 'some_prefix'
    FILTER_LIST = 'dir1, dir2'
    AWS_CLOUDFRONT_DISTRIBUTION = 'E27LVI50CSW06W'
    SYNC_S3_RENAME_GZIP_EXT = '.gz'

.. [1] S3是亚马逊提供的云存储服务,也是目前行业中使用最广泛的云存储服务.2013年底亚马逊云服务才宣布正式入华,估计2014年中旬才能用上.
