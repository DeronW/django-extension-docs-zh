扩展测试服务
=============

:概要: ``runserver_plus`` 命令启动测试服务,并用 Werkzeug_ 作为调试后台


简介
------------

``runserver_plus`` 命令需要安装 `Werkzeug WSGI utilities` . ``Werkzeug`` 是Python的杀手级调试工具,还能调试基于ajax的请求(允许在出错的地方执行代码). 还提供了一个漂亮的错误展示页面.


开始使用
---------------

在启动Django的测试服务时,只要用 ``runserver_plus`` 命令代替 ``runserver`` 命令就可以了::

  $ python manage.py runserver_plus

  * Running on http://127.0.0.1:8000/
  * Restarting with reloader...

  Validating models...
  0 errors found

  Django version 0.97-newforms-admin-SVN-unknown, using settings 'screencasts.settings'
  Development server is running at http://127.0.0.1:8000/
  Using the Werkzeug debugger (http://werkzeug.pocoo.org/)
  Quit the server with CONTROL-C.

提示: ``runserver_plus`` 命令接受原来的所有参数.也就是可以随意指定端口和host,跟原生的 ``runserver`` 命令一模一样.

深入使用
----------

通过 ``runserver_plus`` 命令启动服务后,如果遇到服务代码抛出异常,我们会得到一个 Werkzeug_ 的错误显示页面,而不是默认的Django错误页面.

.. image:: https://f.cloud.github.com/assets/202559/1261027/2637f826-2c22-11e3-83c6-646acc87808b.png
    :alt: werkzeug-traceback

当鼠标划过特定错误堆栈时,还能显示出扩展功能,注意图片右边出现的2个按钮:

.. image:: https://f.cloud.github.com/assets/202559/1261035/558ad0ee-2c22-11e3-8ddd-6678d84d77e7.png
    :alt: werkzeug-options

这几个选项是:

查看源码
^^^^^^^^^^^

这是点击 *显示源码* 后的效果:

.. image:: https://f.cloud.github.com/assets/202559/1261036/583c8c42-2c22-11e3-9eb9-5c16b8732512.png
    :alt: werkzeug-source

产看错误产生的源码有助于快速定位错误原因.抛出异常的部分被高亮显示,这样更方便查看.

有一个不够人性化的地方是,点击 *查看源码* 后,页面没有自动滚动到底部(源码显示的地方),这容易让人觉得什么都没有发生,其实是没有看到.

命令行调试
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

在错误页面上点击命令行调试按钮后,会显示出一个命令行调试工具(网页里面的输入框),是不是屌爆了:

.. image:: https://f.cloud.github.com/assets/202559/1261037/5d12eda6-2c22-11e3-802a-2639ff8813fa.png
    :alt: werkzeug-debugger

这样就回出现一个ajax的命令行调试工具,然后就可以任意发挥了.截图中,在调试框里输入了 ``print environ`` 命令来查看当前环境中给方法传入了哪些参数.

*警告* : 改方法不能被用在人和正式环境中,即使是在正式环境中检测问题时也不行.命令行调试工具允许在服务器端执行Python命令,这是非常危险的.

SSL
^^^

``runserver_plus`` 还支持SSL,这样就可以方便的调试 ``https`` 请求了.使用SSL时需要提供证书的名字,然后 ``runserver_plus`` 会自动生成一个证书::

  $ python manage.py runserver_plus --cert cert
  Validating models...
  0 errors found

  Django version 1.6.dev20130122125534, using settings 'mysite.settings'
  Development server is running at http://127.0.0.1:8000/
  Using the Werkzeug debugger (http://werkzeug.pocoo.org/)
  Quit the server with CONTROL-C.
   * Running on https://127.0.0.1:8000/
   * Restarting with reloader
  Validating models...
  0 errors found

  Django version 1.6.dev20130122125534, using settings 'mysite.settings'
  Development server is running at http://127.0.0.1:8000/
  Using the Werkzeug debugger (http://werkzeug.pocoo.org/)
  Quit the server with CONTROL-C.
  
执行上面的命令后就可以通过 ``https://127.0.0.1:8000`` 在安全模式下访问服务了.在项目目录下会创建2个新的文件,分别是密钥文件和证书文件.重启测试服务时,这2个文件会被保留下来,这样浏览器就不用反复处理证书授权了.如果想使用指定证书文件,可以使用路径参数指向该证书文件::

  $ python manage.py runserver_plus --cert /tmp/cert 
  
使用SSL时需要安装 ``OpenSSL`` 库. ``Werkzeug`` 0.9版本后才允许重用证书文件.通过以下命令安装 ``OpenSSL`` 库::

  $ pip install pyOpenSSL

.. _`Werkzeug WSGI utilities`: http://werkzeug.pocoo.org/
.. _Werkzeug: http://werkzeug.pocoo.org/
