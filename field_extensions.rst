字段扩展
================

:概要: model的字段扩展


当前数据模型的字段的扩展
---------------------------------------

* *AutoSlugField* - 自动生成一个唯一的slug,生成方式是以迭代方式给当前字段后面添加一个随机字符,知道不重复为止.slug生成方式的灵感来自于 SmileyChris 的唯一码生成代码片段.

* *CreationDateTimeField* - DateTimeField类型字段,会自动保存数据第一次被保存到数据库的时间戳.工作方式与添加了 ``auto_now_add=True`` 参数相同,而 ``auto_now_add`` 参数已经不推荐使用.

* *ModificationDateTimeField* - DateTimeField类型字段,当数据出现修改是会自动保存被修改的时间戳.工作方式与添加了 ``auto_now=True`` 参数相同,而 ``auto_now`` 参数已经不推荐使用.

* *UUIDField* - UUIDField for Django, supports all uuid versions which are
  natively supported by the uuid python module.

* *UUIDField* - 唯一标识码字段,通过本地Python模块生成的唯一标识码,支持所有版本的uuid.

* *EncryptedCharField* - 字符串类型字段,会将数据以加密的方式保存和现实,加密方法使用 `Keyczar <http://www.keyczar.org/>`_.使用这个扩展字段时需要安装Keyczar,通过Keyczar库生成加密的密钥,还要在django项目的settings中添加 ``settings.ENCRYPTED_FIELD_KEYS_DIR`` 配置,指向密钥的完整目录.

* *EncryptedTextField* - 字符串类型字段,与 *EncryptedCharField* 字段类似,但是继承自 ``TextField`` 字段.