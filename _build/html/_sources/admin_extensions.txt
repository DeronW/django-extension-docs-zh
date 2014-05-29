admin后台管理扩展
==================

:概要: Admin后台的字段扩展


*ForeignKeyAutocompleteAdmin* - 该扩展字段在Admin后台中显示为一个搜索输入框.前端显示的内容由 ForeignKeySearchInput form的weight渲染,通过jQuery的autocompletion功能实现搜索效果.

用法举例
--------

启用后台管理的自动补全功能，根据示例编辑 ``admin.py`` 文件：

::

    from django.contrib import admin
    from foo.models import Permission
    from django_extensions.admin import ForeignKeyAutocompleteAdmin


    class PermissionAdmin(ForeignKeyAutocompleteAdmin):
        # User is your FK attribute in your model
        # first_name and email are attributes to search for in the FK model
        related_search_fields = {
        'user': ('first_name', 'email'),
        }

        fields = ('user', 'avatar', 'is_active')

        ...

    admin.site.register(Permission, PermissionAdmin)

如果使用了 django-reversion_ ，参考下面的例子：

::

    from django.contrib import admin
    from foo.models import MyVersionModel
    from reversion.admin import VersionAdmin
    from django_extensions.admin import ForeignKeyAutocompleteAdmin

    class MyVersionModelAdmin(VersionAdmin, ForeignKeyAutocompleteAdmin):
        ...

    admin.site.register(MyVersionModel, MyVersionModelAdmin)


.. _django-reversion: https://github.com/etianen/django-reversion
