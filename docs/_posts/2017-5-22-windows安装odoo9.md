## windows源码安装odoo

首先尝试安装node.js ,因为要用到nodejs的npm，借鉴的网站是http://www.jianshu.com/p/4d466ae8ecdf

配置node.js的网站https://segmentfault.com/a/1190000005602881 在中文官网上应该点击winodws的那个图标，不是那个压缩包

安装相应的requriment.txt文件的时候说出了妈的error: Microsoft Visual C++ 9.0 is required (Unable to find vcvarsall.bat). Get it from http://aka.ms/vcpython27

所以果断从那个网上直接下了，网址人家也给了差不多了就

然后安装什么python_ldap报错了，后来根据提示来做的，用的.whl来装的，把其中的一个.whl文件放到了C盘中user中的Default的目录下，然后再次安装whl文件，安装成功，https://www.douban.com/note/484046487/
会报错说有一个DLL找不到，其实先pip uninstall py什么的软件就可以了，然后还有一个什么win32service 的错误，最后在下载一个软件记得是64未(pywin32-221.win-amd64-py2.7.exe)的就可以了，重启OK
![whl文件](https://github.com/yuzp1996/mymaterial/blob/master/odoo%E5%AE%89%E8%A3%85.png?raw=true)

命令行启动	E:\1Projects\odooForChina9.0\odoo-src>python odoo.py -c odooconf.conf
这个配置文件直接配置的我们服务器上的数据库，所以直接用就可以了。用的IDE是PYcharm ,截图如图![pyCharm](https://github.com/yuzp1996/mymaterial/blob/master/Pycharm%E6%88%AA%E5%9B%BE.png?raw=true)


同事总结的如下（其实就是装上requirments中的环境其实就可以了，其实并没有什么，需要解决的问题就是可能各种库的安装有问题，找方法安装上就行了）

###### 1、升级pip
pip install --upgrade pip
######2、安装python-ldap（下载地址http://www.lfd.uci.edu/~gohlke/pythonlibs/）
python_ldap-2.4.38-cp27-cp27m-win_amd64.whl
###### 3、进入odooForChina9.0/odoo-src下，执行命令
将requirements.txt文件中python-ldap==2.4.19改成python-ldap==2.4.38
pip install -r requirements.txt
###### 4、安装psycopg2
pip install psycopg2
###### 5、安装pywin32-221.win-amd64-py2.7.exe
###### 6、创建postgresql超级用户
###### 7、安装node.js
###### 8、安装node-lessc，和nodejd-legacy
在node目录下执行命令npm install -g less@latest
		npm install -g legacy@latest

