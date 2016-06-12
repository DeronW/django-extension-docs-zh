Model 字段扩展
================

:概要: 数据模型Model的字段扩展

当前数据模型的字段的扩展
---------------------------------------

* ``AutoSlugField`` - 自动生成一个唯一的slug,生成方式是以迭代方式给当前字段后面添加一个随机字符,知道不重复为止.slug生成方式的灵感来自于 SmileyChris 的唯一码生成代码片段.

* ``RandomCharField`` - 自动生成一个指定长度的全局唯一随即字符串. 默认包含数字并区分大小写. 长度为8时, 大约有340万种组合, 长度为12时, 大约有20亿中组合. 参考示例::

    >>> RandomCharField(length=8, unique=True)
    BVm9GEaE

    >>> RandomCharField(length=4, include_alpha=False)
    7097

    >>> RandomCharField(length=12, include_punctuation=True)
    k[ZS.TR,0LHO

    >>> RandomCharField(length=12, lowercase=True, include_digits=False)
    pzolbemetmok

* ``CreationDateTimeField`` - DateTimeField类型字段,会自动保存数据第一次被保存到数据库的时间戳.工作方式与添加了 ``auto_now_add=True`` 参数相同,而 ``auto_now_add`` 参数已经不推荐使用.

* ``ModificationDateTimeField`` - DateTimeField类型字段,当数据出现修改是会自动保存被修改的时间戳.工作方式与添加了 ``auto_now=True`` 参数相同. 保存时将update_modified参数设置为False则本次保存不会更新时间戳::

    >>> example = MyTimeStampedModel.objects.get(pk=1)

    >>> print example.modified
    datetime.datetime(2016, 3, 18, 10, 3, 39, 740349, tzinfo=<UTC>)

    >>> example.save(update_modified=False)

    >>> print example.modified
    datetime.datetime(2016, 3, 18, 10, 3, 39, 740349, tzinfo=<UTC>)

    >>> example.save()

    >>> print example.modified
    datetime.datetime(2016, 4, 8, 14, 25, 43, 123456, tzinfo=<UTC>)

也可以直接通过设置实例属性的方式, 禁止自动更新时间戳::

    >>> example = MyCustomModel.objects.get(pk=1)

    >>> print example.modified
    datetime.datetime(2016, 3, 18, 10, 3, 39, 740349, tzinfo=<UTC>)

    >>> example.update_modified=False

    >>> example.save()

    >>> print example.modified
    datetime.datetime(2016, 3, 18, 10, 3, 39, 740349, tzinfo=<UTC>)

* ``UUIDField`` - 唯一标识码字段,通过当前系统的Python模块生成的唯一标识码.

  .. deprecated:: 1.4.7
     Django 1.8 开始支持原生UUIDField字段. Django-Extensions会支持这个字段直到 Django1.7不再维护.

* ``PostgreSQLUUIDField`` - uid字段, 使用了PostgreSQL的uuid类型.

  .. deprecated:: 1.4.7
     Django 1.8 开始支持原生UUIDField字段. Django-Extensions会支持这个字段直到 Django1.7不再维护.

* ``EncryptedCharField`` - 字符串类型字段,会将数据以加密的方式保存和现实,加密方法使用 `Keyczar <http://www.keyczar.org/>`_.使用这个扩展字段时需要安装Keyczar,通过Keyczar库生成加密的密钥,还要在django项目的 ``settings.py`` 中添加 ``settings.ENCRYPTED_FIELD_KEYS_DIR`` 配置,指向密钥的完整目录.

* ``EncryptedTextField`` - 字符串类型字段,与 ``EncryptedCharField`` 字段类似,但是继承自 ``TextField`` 字段.

* ``ShortUUIDField`` - 字符串类型字段，将生成的uuid转换成较短的字符串（好像是57进制）。生成字符串结果的长度小于22位，通过参数可以生成更短的字符长度，短长度字符虽然不能保证绝对的唯一性，但重复的概率极低

* ``JSONField`` - 基于TextField类型, 并支持JSON的序列化和反序列化.