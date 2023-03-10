<!--ts-->

- [实战笔记](#实战笔记)

<!-- Added by: edy, at: 2023年 2月 3日 星期五 12时43分28秒 CST -->

<!--te-->

# 实战笔记

通过 `requirements.txt` 离线安装依赖包

背景：

目前一个机器环境上，需要离线安装一些依赖包（这里自己本机笔记），具体安装包和版本可见：`requirements.txt`

```bash
# 随便创建一个pkgs目录(/Users/tt/Desktop/pkgs)，用来收集所有pkg离线安装包(下载后都放在这里)
mkdir -p ~/Desktop/pkgs

# 依照项目里requirements.txt，下载pkg安装包
# 注意：这些离线包通过命令下载来的，也可以直接去官网直接下载 xxx.whl，或 xxx.tar.gz 文件，用于安装，过程都一样。
pip download -r requirements.txt -d /Users/tt/Desktop/pkgs

# 查看下载了哪些pkg安装包(有的是：xxx.whl, 有的是：xxx.tar.gz)
cd /Users/tt/Desktop/pkgs/
ls -rtl

# 将这个目录压缩打包，想法子弄到自己的服务器上(这里，自己造一个干净的虚拟环境，测试步骤)

# 目前有一个感觉的虚拟环境(--no-site-packages)，名为：pkg_py370
(pkg_py370) lyfdeMacBook-Pro:~ tt$ pip list
Package    Version
---------- -------
pip        19.3.1
setuptools 42.0.2
wheel      0.33.6

# 查看自己依赖包管理目录在哪
(pkg_py370) lyfdeMacBook-Pro:~ tt$ pip -V
pip 19.3.1 from /Users/tt/.workspaces/pkg_py370/lib/python3.7/site-packages/pip (python 3.7)

# 前往此目录，看看目前有哪些已安装的依赖包了
cd /Users/tt/.workspaces/pkg_py370/lib/python3.7/site-packages/

(pkg_py370) lyfdeMacBook-Pro:site-packages tt$ ls -rtl
total 8
-rw-r--r--   1 tt  staff   126 12 25 17:59 easy_install.py
drwxr-xr-x   3 tt  staff    96 12 25 17:59 __pycache__
drwxr-xr-x  44 tt  staff  1408 12 25 17:59 setuptools
drwxr-xr-x   7 tt  staff   224 12 25 17:59 pkg_resources
drwxr-xr-x  11 tt  staff   352 12 25 17:59 setuptools-42.0.2.dist-info
drwxr-xr-x   7 tt  staff   224 12 25 17:59 pip
drwxr-xr-x   9 tt  staff   288 12 25 17:59 pip-19.3.1.dist-info
drwxr-xr-x  12 tt  staff   384 12 25 17:59 wheel
drwxr-xr-x   9 tt  staff   288 12 25 17:59 wheel-0.33.6.dist-info

# 可以发现，和pip list 显示一样，目前有：setuptools, pip, wheel

# ok，开始离线安装新的依赖包，首先进入收集的离线安装包目录(/Users/tt/Desktop/pkgs/: 有的是：xxx.whl, 有的是：xxx.tar.gz)
# 注意：这里说明下：

# xxx.whl:
# 	1. 此类安装包文件，有的使用多种系统，有的是仅某一系统适用(如：mac_os).
# 	2. 所以需要在google搜索：pip install xxx，找到官网.
# 	3. 在包的官网中，点击左边的 "Download files"，会出现很多安装包.
# 	4. 下载需要系统的xxx.whl即可。
# xxx.tar.gz:
# 	1. 此类安装包文件，就厉害了，是源码安装包，任何系统都行。
# 	2. 所以需要在google搜索：pip install xxx，找到官网.
# 	3. 在包的官网中，点击左边的 "Download files"，会出现很多安装包.
# 	4. 下载此包的 xxx.tar.gz 文件.
# 	5. 在需要安装的服务器上，python安装完毕，如果没有setup包，需要提前安装。
# 	6. 安装 xxx:
# 		1. 先解压：tar -x xxx.tar.gz
# 		2. cd xxx
# 		3. 执行安装：python setup.py install  或  python3 setup.py install，即可安装。

(pkg_py370) lyfdeMacBook-Pro:site-packages tt$ cd ~/Desktop/pkgs/

# 如：安装Django(xxx.whl文件)为例，测试时可以将网wifi关掉，确保是没连接外网

# 安装Django，失败报错
(pkg_py370) lyfdeMacBook-Pro:pkgs tt$ pip install Django-2.1.4-py3-none-any.whl
Processing ./Django-2.1.4-py3-none-any.whl
WARNING: Retrying (Retry(total=0, connect=None, read=None, redirect=None, status=None)) after connection broken by 'NewConnectionError('<pip._vendor.urllib3.connection.VerifiedHTTPSConnection object at 0x10ae2a978>: Failed to establish a new connection: [Errno 8] nodename nor servname provided, or not known')': /simple/pytz/
ERROR: Could not find a version that satisfies the requirement pytz (from Django==2.1.4) (from versions: none)
ERROR: No matching distribution found for pytz (from Django==2.1.4)

# 报错了，因为在安装Django时，需要一个 "前提依赖包pytz" ，平时联网时会自动去下载pytz的whl。
# 那怎么办呢？要知道 requirements.txt 是全部的包，所以，直接先安装上 pytz 即可。

# 先安装 pytz
(pkg_py370) lyfdeMacBook-Pro:pkgs tt$ pip install pytz-2019.3-py2.py3-none-any.whl
Processing ./pytz-2019.3-py2.py3-none-any.whl
Installing collected packages: pytz
Successfully installed pytz-2019.3

# 再次安装 Django，成功
(pkg_py370) lyfdeMacBook-Pro:pkgs tt$ pip install Django-2.1.4-py3-none-any.whl
Processing ./Django-2.1.4-py3-none-any.whl
Requirement already satisfied: pytz in /Users/tt/.workspaces/pkg_py370/lib/python3.7/site-packages (from Django==2.1.4) (2019.3)
Installing collected packages: Django
Successfully installed Django-2.1.4

# 此时在看安装的依赖包，已经有了
(pkg_py370) lyfdeMacBook-Pro:pkgs tt$ pip freeze
Django==2.1.4
pytz==2019.3

# 其他安装包，都这样安装即可。注意：有的是：xxx.tar.gz离线包，怎么安装呢？一样
# xxx.tar.gz，也直接install 就行
#
# 因为install操作后，它会和平时其他离线下载xx.tar.gz，在解压进入xx文件目录，使用setup 离线安装一样，直接pip install 就行，这里不用解压

# 如：安装pycparser，收集来的是：pycparser-2.19.tar.gz

(pkg_py370) lyfdeMacBook-Pro:pkgs tt$ pip install pycparser-2.19.tar.gz
Processing ./pycparser-2.19.tar.gz
Building wheels for collected packages: pycparser
  Building wheel for pycparser (setup.py) ... done
  Created wheel for pycparser: filename=pycparser-2.19-py2.py3-none-any.whl size=111029 sha256=eb46575363d5c7c0392fc020433d470b4d39831faf15c0050da733c3ba201cb9
  Stored in directory: /Users/tt/Library/Caches/pip/wheels/4f/37/2d/0361842459de8b73f3c9507201f8c1b9639ad716ea089a974d
Successfully built pycparser
Installing collected packages: pycparser
Successfully installed pycparser-2.19

# 注意：收集离线安装pkg的目录随意，但用哪一个pip安装，则这些依赖包就会安装到哪一个 "pip -V" 所在目录下。
# 所以，如果想在其他虚拟环境下安装这些包，需要先切换至相应虚拟环境下，使用pip安装。
# 当然不切换进入虚拟环境也行，指定pip的绝对路径也行，哈哈哈，一样的。

# 最后，我们再看看已安装哪些包：
(pkg_py370) lyfdeMacBook-Pro:pkgs tt$ pip freeze
cffi==1.13.2
cryptography==2.8
Django==2.1.4
django-cors-headers==3.2.0
django-filter==2.2.0
django-mysql==2.4.1
djangorestframework==3.10.3
djangorestframework-jwt==1.11.0
Pillow==6.2.1
pycparser==2.19
PyJWT==1.7.1
PyMySQL==0.9.3
pytz==2019.3
six==1.13.0

# 看看是不是都安装到 "pip -V" 所在目录了呢？
(pkg_py370) lyfdeMacBook-Pro:pkgs tt$ cd /Users/tt/.workspaces/pkg_py370/lib/python3.7/site-packages/
(pkg_py370) lyfdeMacBook-Pro:site-packages tt$ ls -rtl
total 872
-rw-r--r--    1 tt  staff     126 12 25 17:59 easy_install.py
drwxr-xr-x   44 tt  staff    1408 12 25 17:59 setuptools
drwxr-xr-x    7 tt  staff     224 12 25 17:59 pkg_resources
drwxr-xr-x   11 tt  staff     352 12 25 17:59 setuptools-42.0.2.dist-info
drwxr-xr-x    7 tt  staff     224 12 25 17:59 pip
drwxr-xr-x    9 tt  staff     288 12 25 17:59 pip-19.3.1.dist-info
drwxr-xr-x   12 tt  staff     384 12 25 17:59 wheel
drwxr-xr-x    9 tt  staff     288 12 25 17:59 wheel-0.33.6.dist-info
drwxr-xr-x   10 tt  staff     320 12 25 18:10 pytz
drwxr-xr-x   11 tt  staff     352 12 25 18:10 pytz-2019.3.dist-info
drwxr-xr-x   22 tt  staff     704 12 25 18:10 django
drwxr-xr-x   11 tt  staff     352 12 25 18:10 Django-2.1.4.dist-info
drwxr-xr-x   45 tt  staff    1440 12 25 18:16 rest_framework
drwxr-xr-x    8 tt  staff     256 12 25 18:16 djangorestframework-3.10.3.dist-info
drwxr-xr-x   13 tt  staff     416 12 25 18:17 jwt
drwxr-xr-x   10 tt  staff     320 12 25 18:17 PyJWT-1.7.1.dist-info
drwxr-xr-x   13 tt  staff     416 12 25 18:17 rest_framework_jwt
drwxr-xr-x    9 tt  staff     288 12 25 18:17 djangorestframework_jwt-1.11.0.dist-info
drwxr-xr-x   18 tt  staff     576 12 25 18:17 django_filters
drwxr-xr-x    8 tt  staff     256 12 25 18:17 django_filter-2.2.0.dist-info
drwxr-xr-x   20 tt  staff     640 12 25 18:18 django_mysql
drwxr-xr-x    8 tt  staff     256 12 25 18:18 django_mysql-2.4.1.dist-info
drwxr-xr-x    9 tt  staff     288 12 25 18:18 corsheaders
drwxr-xr-x    8 tt  staff     256 12 25 18:18 django_cors_headers-3.2.0.dist-info
drwxr-xr-x   17 tt  staff     544 12 25 18:19 pymysql
drwxr-xr-x    9 tt  staff     288 12 25 18:19 PyMySQL-0.9.3.dist-info
drwxr-xr-x   16 tt  staff     512 12 25 18:19 pycparser
drwxr-xr-x    8 tt  staff     256 12 25 18:19 pycparser-2.19.dist-info
-rw-r--r--    1 tt  staff   33045 12 25 18:23 six.py
drwxr-xr-x    4 tt  staff     128 12 25 18:23 __pycache__
drwxr-xr-x    8 tt  staff     256 12 25 18:23 six-1.13.0.dist-info
-rw-r--r--    1 tt  staff  405376 12 25 18:23 _cffi_backend.cpython-37m-darwin.so
drwxr-xr-x   23 tt  staff     736 12 25 18:23 cffi
drwxr-xr-x    9 tt  staff     288 12 25 18:23 cffi-1.13.2.dist-info
drwxr-xr-x   10 tt  staff     320 12 25 18:23 cryptography
drwxr-xr-x   12 tt  staff     384 12 25 18:23 cryptography-2.8.dist-info
drwxr-xr-x  103 tt  staff    3296 12 25 18:24 PIL
drwxr-xr-x    9 tt  staff     288 12 25 18:24 Pillow-6.2.1.dist-info

# ok，安装完毕，至于验证，在进入python里，导入模块看看就知道了。

# 如，随便测试一个 Pillow 包，是否正常使用，导包正常，没报错。
(pkg_py370) lyfdeMacBook-Pro:site-packages tt$ python
Python 3.7.0 (default, Oct  8 2019, 18:54:48)
[Clang 10.0.1 (clang-1001.0.46.4)] on darwin
Type "help", "copyright", "credits" or "license" for more information.
>>> from PIL import Image
>>>

# 离线安装到此结束了

# 备注:
# 还有一个非常规操作，直接将安装好的，可以使用的包，复制一份放进 "pip -V" 所在目录里，也行，只要能在python环境中正常使用就行。（但要注意:python版本环境是一样的，比如:都是ubuntu系统，python3.6.6版本）
```
