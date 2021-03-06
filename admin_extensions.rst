Admin 后台管理扩展
=====================

:概要: Admin后台的字段扩展


*ForeignKeyAutocompleteAdmin* - 该扩展字段在Admin后台中显示为一个搜索输入框.
前端显示的内容由 ForeignKeySearchInput form的weight渲染, 
通过jQuery的autocompletion功能实现搜索效果.

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

如果想要限制搜索功能中的自动匹配, 覆写admin的 ``get_related_filter`` 方法.
例如, 添加一条限制给非管理员用户: 仅能向自己创建的文章中添加附件

::

    class AttachmentAdmin(ForeignKeyAutocompleteAdmin):

        ...

        def get_related_filter(self, model, request):
            user = request.user
            if not issubclass(model, Article) or user.is_superuser():
                return super(AttachmentAdmin, self).get_related_filter(
                    model, request
                )
            return Q(owner=user)

注意, 某些恶意操作可以绕过这种使用限制(例如一个经过精心构造的伪装请求)

.. _django-reversion: https://github.com/etianen/django-reversion
