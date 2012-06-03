.. pythonbrew documentation master file, created by
   sphinx-quickstart on Sat Jun  2 09:35:56 2012.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

欢迎阅读pythonbrew文档
======================

在$HOME目录中管理python安装

简介
----

pythonbrew是受 `perlbrew <http://github.com/gugod/App-perlbrew>`_ 和 `rvm <https://github.com/wayneeseguin/rvm>`_ 启发，在用户的$HOME目录中进行python构建和安装自动化的项目。

*另一衍生版本* ： `pythonz <https://github.com/saghul/pythonz>`_ 。

安装
----

|

建议使用如下语句下载安装pythonbrew::

    $ curl -kL http://xrl.us/pythonbrewinstall | bash

pythonbrew就会安装到 ``~/.pythonbrew`` 。

|

然后在您的 ``~/.bashhrc`` 文件追加下面这一行::

    $ [[ -s $HOME/.pythonbrew/etc/bashrc ]] && source $HOME/.pythonbrew/etc/bashrc

|

设置PYTHONBREW_ROOT环境变量可以pythonbrew安装到指定目录::

    $ export PYTHONBREW_ROOT=/path/to/pythonbrew
    $ curl -kLO http://xrl.us/pythonbrewinstall
    $ chmod +x pythonbrewinstall
    $ ./pythonbrewinstall


系统层(多用户环境)安装
----------------------

在root用户环境下运行安装脚本，将自动将pythonbrew安装到 `` /usr/local/pythonbrew`` ，并为系统下的每个用户进行配置。

安装完成后，非root用户在使用pythonbrew就不必调用sudo，而是直接运行 ``sudosudopybrew`` 即可::

    $ sudopybrew install -n -v -j2 2.7.2


用法
----

一般用法是::

    pythonbrew command [options]

|

安装不同版本的python::

    pythonbrew install 2.7.2
    pythonbrew install --verbose 2.7.2
    pythonbrew install --test 2.7.2
    pythonbrew install --test --force 2.7.2
    pythonbrew install --configure="CC=gcc_4.1" 2.7.2
    pythonbrew install --no-setuptools 2.7.2
    pythonbrew install http://www.python.org/ftp/python/2.7/Python-2.7.2.tgz
    pythonbrew install /path/to/Python-2.7.2.tgz
    pythonbrew install /path/to/Python-2.7.2
    pythonbrew install 2.7.2 3.2

|

永久性地使用某个特定版本的python(即每次登录shell都使用某个版本的python)::
    
    pythonbrew switch 2.7.2
    pythonbrew switch 3.2

|

临时性地切换使用某个特定版本的python(即在当前shell中使用某个版本的python)::

    pythonbrew use 2.7.2

|

可以使用系统内所有版本/某个指定版本的python运行某个python文件::

    pythonbrew py test.py
    pythonbrew py -v test.py # 显示详细的输出结果
    pythonbrew py -p 2.7.2 -p 3.2 test.py # 使用指定版本的python

|

列出系统内所有已安装的各个版本的python::

    pythonbrew list

|

列出pythonbrew可以安装哪些版本的python::

    pythonbrew list -k

|

删除某个特定版本的python::

    pythonbrew uninstall 2.7.2
    pythonbrew uninstall 2.7.2 3.2

|

清理陈旧的源码目录和档案包::

    pythonbrew cleanup

|

升级到pythonbrew到最新版本::

    pythonbrew update
    pythonbrew update --master
    pythonbrew update --develop

|

禁用pythonbrew(即切换回原始环境)::

    pythonbrew off

|

创建或移除指向某个python版本的符号链接(在您的$PATH中的某个目录)::

    pythonbrew symlink # 为已安装的各个版本的python都创建一个符号链接，形如"py2.7.2"。
    pythonbrew symlink -p 2.7.2
    pythonbrew symlink pip #创建指向bin目录下某个指定脚本的符号链接。
    pythonbrew symlink -r # 移除符号链接。
    pythonbrew symlink -v foo # 创建指向bin目录下某个指定的隔离环境的符号链接。

|

在当前或是某个特定版本的python中运行 ``buildout`` ::

    pythonbrew buildout
    pythonbrew buildout -p 2.6.6

|

创建python隔离环境(借助virtualenv) ::

    pythonbrew venv init
    pythonbrew venv create proj
    pythonbrew venv list
    pythonbrew venv use proj
    pythonbrew venv delete proj
    pythonbrew venv rename proj proj2

| 

查看版本 ::

    pythonbrew version


命令
----

``install <version>``
    构建并安装某个给定版本的python，并自动安装setuptools和pip。

``switch <version>``
    永久切换到某个特定版本的python做为默认版本。

``use <version>``
    在当前shell下使用某个特定版本的python。

``py <python file>``
    使用所有版本/某个特定版本运行一个python文件。

``list``
    列出所有已安装的python版本。

``list -k <version>``
    列出所有可安装的python版本。

``uninstall <version>``
    删除某个特定版本的python。

``cleanup``
    移除陈旧的源码目录和档案包。

``update``
    升级pythonbrew到最新版本。

``off``
    禁用pythonbrew。

``symlink``
    创建或移除指向某个python版本的符号链接(在您的$PATH中的某个目录)。

``buildout``
    在当前或是某个特定版本的python中运行 ``buildout`` 。

``venv``
    创建python隔离环境(借助virtualenv)。

``version``
    查看版本。

查看更多细节，可以运行::

    $ pythonbrew help <command>


相关文档和链接
--------------

* `Python 的虛擬環境及多版本開發利器─Virtualenv 與 Pythonbrew
  <http://www.openfoundry.org/tw/tech-column/8516-pythons-virtual-environment-and-multi-version-programming-tools-virtualenv-and-pythonbrew>`_ 。

* `Pythonbrew – 讓環境得以快速切換不同的Python版本
  <http://antbsd.twbbs.org/~ant/wordpress/?p=3832>`_ 。

授权
----

MIT 开源协议

Copyright (c) <2010-2012> <utahta>

任何人都可以免费权限该软件和相关文档的副本，在处理软件上不受任何限制，包括但不限于使用，复制，修改，合并，发布，分发，转授和出售本软件的副本，
以及再授权等等，但获得以上权利必须履行以下义务

 **在软件和软件的所有副本中都必须包含版权声明和许可声明。** 





.. toctree::
   :maxdepth: 2

