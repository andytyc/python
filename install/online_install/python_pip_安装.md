<!--ts-->

- [在线](#在线)
  - [ubuntu](#ubuntu)
    - [系统-初始环境](#系统-初始环境)
    - [查看-最初的 python 环境](#查看-最初的python环境)
    - [安装 pip](#安装pip)
    - [更新 pip 源-国内源](#更新pip源-国内源)
      - [临时](#临时)
      - [永久](#永久)
    - [安装 python-多个指定版本](#安装python-多个指定版本)
      - [安装 python3.7.0](#安装python370)
      - [安装 python3.6.6](#安装python366)
    - [安装 virtualenv-虚拟环境](#安装virtualenv-虚拟环境)
      - [virtualenv-安装](#virtualenv-安装)
      - [virtualenv-使用](#virtualenv-使用)
      - [virtualenvwrapper-安装](#virtualenvwrapper-安装)
      - [virtualenvwrapper-使用](#virtualenvwrapper-使用)
        - [环境变量-配置](#环境变量-配置)
        - [使用](#使用)

<!-- Added by: tt, at: Fri Feb 28 15:00:57 CST 2020 -->

<!--te-->

# 在线

## ubuntu

- 以在阿里云上，申请一台 ecs 服务器，选择 ubuntu 系统后，进行的如下测试执行。

### 系统-初始环境

```bash
# 1. ubuntu更新源(软件包管理工具)，改为国内。
见：github/tool/servers/01_ubuntu_xxx.md

# 2. 注意，要进行下更新哦。
sudo apt-get update

---
注意：
一般任何一个系统呢，都需要安装一些必要的依赖包(软件包)，这里需要安装什么呢？先不说，下边出现什么报错？咱们再安装即可。

如，一般安装这些：
sudo apt-get install zlib1g-dev libffi-dev zip unzip
```

### 查看-最初的 python 环境

```bash
# 查看这台ubuntu, 当前python环境情况(这台ubuntu服务器，最初的配置情况)
which python
which python3
python -V
python3 -V
pip -V
pip3 -V

root@iZ2zefl9xsei39b00juvmoZ:~# which python
/usr/bin/python

root@iZ2zefl9xsei39b00juvmoZ:~# which python3
/usr/bin/python3

root@iZ2zefl9xsei39b00juvmoZ:~# pip -V
pip 9.0.1 from /usr/lib/python2.7/dist-packages (python 2.7)

root@iZ2zefl9xsei39b00juvmoZ:~# pip3 -V
Command 'pip3' not found, but can be installed with:
apt install python3-pip

---
注意：
这里发现没有pip3，那么 <如果我们需要> 使用pip3(python3对应的pip3)如何安装呢？方法：
>>>
方法1: (注意更新ubuntu更新源)：
解释：虽然以后可能安装其他的python3版本，但我们为系统自带的python3安装pip3，配套整理(不乱)。
apt install python3-pip

方法1，若安装失败？解决办法采用 方法2 即可。

方法2：
1. 先下载安装pip的脚本
wget https://bootstrap.pypa.io/get-pip.py

2. 再执行命令, 安装pip即可。
注意：
    使用 python3(对应python3.6.9) 执行此脚本get-pip.py后，会安装pip3。
    而，使用 python(对应python2.7.17) 执行此脚本get-pip.py后，会安装pip。
python3 get-pip.py

---
安装pip3完毕。
```

### 安装 pip

```bash
# 方法1：
sudo apt install python-pip                安装pip(对应python -- which python 或 python -V)
sudo apt install python3-pip                安装pip3(对应python3 -- which python3 或 python3 -V)

# 方法2：
1. 先下载安装pip的脚本
wget https://bootstrap.pypa.io/get-pip.py

2. 再执行命令安装pip即可。
注意：
    2.1 使用 python(python -V) 执行此脚本get-pip.py后，会安装pip。
    2.2 若使用 python3(python3 -V) 执行此脚本get-pip.py后，会安装pip3。

python get-pip.py               安装pip
python3 get-pip.py              安装pip3

---
# 查看pip情况，如：
root@iZ2zefl9xsei39b00juvmoZ:~# pip3 -V
pip 9.0.1 from /usr/lib/python3/dist-packages (python 3.6)

root@iZ2zefl9xsei39b00juvmoZ:~# pip -V
pip 9.0.1 from /usr/lib/python2.7/dist-packages (python 2.7)
```

### 更新 pip 源-国内源

#### 临时

```
临时指定pip源路径，无需配置pip源, -i 参数
pip install xxname -i https://pypi.douban.com/simple
```

#### 永久

```
# 修改pip源为国内源，目的为 pip install 加快速度

---------- 1. 配置好pip源文件 ----------
创建目录
mkdir /root/.pip/

编辑pip源-配置文件
vim /root/.pip/pip.conf
"""
[global]
trusted-host=mirrors.aliyun.com
index-url=http://mirrors.aliyun.com/pypi/simple/
"""

---------- 2. 如何使用呢？ ----------
# 之后，要更新任意python版本的pip源为国内源，只需将 `相应版本的pip` 进行更新即可, 如：
/usr/local/python370/bin/pip3 install --upgrade pip

---
若，发现没作用，可从如下想想：
    1. 可能指定的 国内源 无效；
    2. 可能虚拟环境创建时，原版本的pip没更新 pip源 ，是不是会影响虚拟环境里的pip也是没指向国内呢？
```

### 安装 python-多个指定版本

#### 安装 python3.7.0

```
# 背景：
1. 现在服务器上，python ->> python2.7.17, python3 ->> python3.6.9
2. 现在希望，再安装一个版本：python3.7.0
3. ubuntu服务器是新的，有些系统依赖包没安装，所以最开始安装时，会各种报错，没关系，安装需要的包即可。


# 来到 root 目录下，创建downloads目录，管理自己下载的一些工具/软件包等。
cd
mkdir downloads
cd downloads

# 下载Python 3.7.0
wget -c https://www.python.org/ftp/python/3.7.0/Python-3.7.0.tar.xz

# 解压
tar -xvf Python-3.7.0.tar.xz
cd Python-3.7.0/

# 此处，编译说明下：
# --prefix=: 指定安装目录(此目录不存在，会自动创建)；
# install -- 注意事项(区别：altinstall(次要)):
    >> 通过查看 cat README.rst 文件里，`Installing multiple versions`这一栏的描述(可谷歌翻译下)，可知道如下描述情景。
    1. 多版本安装在一个前缀(--prefix)目录下时，为避免其他版本安装覆盖，需要指明哪一个为主要版本，哪些为次要版本；
    2. 比如：`--prefix=/usr/local/python37` 目录下，以后安装 3.7.0, 3.7.1, 3.7.2 等多个版本时。
    3. 在编译安装时，谁执行的 `make altinstall` 表示作为 `次要版本`，使用时需指明那个版本：`${prefix}/bin/pythonX.Y`.
    4. 在编译安装时，谁执行的 `make install` 表示 `主要版本`，即此目录下 `${prefix}/bin/python3` 会指向此版本的 `${prefix}/bin/pythonX.Y`.
    >> 所以，有时有人在同一个 --prefix 下安装其他版本(多版本)python时，使用 altinstall, 不使用install(否则会报错).

# 编译并安装 - (&&: shell多个命令先后执行，也可以将这三个命令，分别一行一行执行)
./configure --prefix=/usr/local/python370 && make && make install

---- 处理报错 ----
# 报错1：
zipimport.ZipImportError: can't decompress data; zlib not available
Makefile:1122: recipe for target 'install' failed
make: *** [install] Error 1

# 原因提示，ubuntu缺少依赖包：zlib，安装即可：
sudo apt-get install zlib1g-dev

# 重新编译安装
./configure --prefix=/usr/local/python370 && make && make install

--- 重新执行编译，再次报错 ---
# 报错2：
ModuleNotFoundError: No module named '_ctypes'
Makefile:1122: recipe for target 'install' failed
make: *** [install] Error 1

# 原因发现，ubuntu缺少依赖包：libffi，进行安装：
sudo apt install libffi-dev

# 重新编译安装
./configure --prefix=/usr/local/python370 && make && make install
... ...
Collecting setuptools
Collecting pip
Installing collected packages: setuptools, pip
Successfully installed pip-10.0.1 setuptools-39.0.1

--- 解决错误，编译安装成功 ---

# 验证安装，打印版本
root@iZ2zefl9xsei39b00juvmoZ:~/downloads/Python-3.7.0# /usr/local/python370/bin/python3 -V
Python 3.7.0

--------------- 到此为止，python3.7.0成功安装完毕 ---------------

--------------- 如需要，将 pip源 更新下 ---------------
# 修改pip源为国内源，目的为 pip install 加快速度
mkdir /root/.pip/

vim /root/.pip/pip.conf
"""
[global]
trusted-host=mirrors.aliyun.com
index-url=http://mirrors.aliyun.com/pypi/simple/
"""

# 更新pip
/usr/local/python370/bin/pip3 install --upgrade pip
```

#### 安装 python3.6.6

```bash
# 安装了python3.7.0, 还想再安装一个版本(~_<)，python3.6.6 玩玩.
# 注意：
    1. 因为ubuntu是新的机器，老司机们一般都会对机器提前安装些依赖包，而我没有，所以上边在编译时报了两次错误。
    2. 那么，既然现在已经安装了一些必要依赖包，在尝试安装一个版本，看看编译是否还会报错呢？(当然就不会再报错了)


# 切至下载目录
cd /root/downloads/

# 下载
wget -c https://www.python.org/ftp/python/3.6.6/Python-3.6.6.tar.xz

# 解压，并进入目录
tar -xvf Python-3.6.6.tar.xz
cd Python-3.6.6/

# 编译并安装
./configure --prefix=/usr/local/python366
make
make install
或者, 通过一句命令实现执行 `./configure --prefix=/usr/local/python366 && make && make install`

# 验证安装，打印版本
root@iZ2zefl9xsei39b00juvmoZ:~/downloads/Python-3.6.6# /usr/local/python366/bin/python3 -V
Python 3.6.6

--------------- 再次安装的 python3.6.6 一气呵成，ok ---------------
```

### 安装 virtualenv-虚拟环境

#### virtualenv-安装

```bash
# 背景：
1. 此时系统版本 python(python2.7.17-pip), python3(python3.6.9-pip3), 后来额外安装了两个版本：python3.7.0, python3.6.6.
2. 现在要安装一个 virtualenv ，来创建虚拟环境，用于开发项目的测试、部署。


方法1(推荐-自己也常采用-因为pip系统自带)：
pip install virtualenv      通过pip安装(对应python2.7.17), 因为如果以后接手一台服务器，可能没安装python3但python2.7.x自带的(必有)。

方法2：
pip3 install virtualenv     通过pip3安装(此时安装了pip3)

方法3：
apt-get install python-virtualenv      ubuntu系统中, 也可以通过apt管理工具安装virtualenv


# 验证安装(采用了方法1)，查看版本
root@iZ2zefl9xsei39b00juvmoZ:~# virtualenv --version
virtualenv 20.0.7 from /usr/local/lib/python2.7/dist-packages/virtualenv/__init__.pyc

---
# 相关查看virtualenv命令：
pip freeze  或  pip3 freeze
```

#### virtualenv-使用

```bash
# 在 /opt/ 目录下，创建一个目录 venv 来统一收集以后自己创建的所有虚拟环境.
mkdir /opt/venv
cd /opt/venv/

# 在这个目录venv下，创建一个独立的Python运行环境，命名为test_py366:
virtualenv --no-site-packages -p /usr/local/python366/bin/python3 test_py366

------------------------ 报错处理 ------------------------
# 报错：
virtualenv: error: unrecognized arguments: --no-site-packages

# 原因-解决：
github/virtualenv/issue 里发现，有网友和官方讨论：
最新版本的virtualenv, 有问题，官方已经收到举报，建议将版本降至：16.7.9
pip install --upgrade virtualenv==16.7.9

# 此时再次创建试试，在目录venv下，创建一个独立的Python运行环境，命名为test_py366:
virtualenv --no-site-packages -p /usr/local/python366/bin/python3 test_py366

# venv下，创建虚拟环境 test_py366 成功。

------------------------ 问题解决, ok ------------------------

# 进入虚拟环境试试：
root@iZ2zefl9xsei39b00juvmoZ:~# source /opt/venv/test_py366/bin/activate
(test_py366) root@iZ2zefl9xsei39b00juvmoZ:~#

# 退出
(test_py366) root@iZ2zefl9xsei39b00juvmoZ:~# deactivate
```

#### virtualenvwrapper-安装

- virtualenvwrapper, 是 virtualenv 的管理工具，让用户使用起来更加方便快捷。

```bash
# 安装 virtualenvwrapper

方法1(推荐-自己常采用-pip系统自带)：
pip install virtualenvwrapper       通过 pip 安装的(python2.7.17的pip, 即：pip -V)

方法2：
pip3 install virtualenvwrapper      通过 pip3 安装的(python3.6.9的pip, 即：pip3 -V)


# 解释：
如果此时还没有安装 virtualenv ，没关系安装 virtualenvwrapper 时，也会同时将 virtualenv 安装。

# 采用方法1，安装完毕
/usr/local/bin 目录下, 会发现除了 virtualenv 外，安装上了 virtualenvwrapper.sh.
```

#### virtualenvwrapper-使用

##### 环境变量-配置

```bash
# 首先，配置环境变量，然后就可以通过 命令 来快速管理、控制虚拟环境了.

# 第一步，需准备如下3个资料：
    1. python环境(VIRTUALENVWRAPPER_PYTHON)：自己采用的方法1安装，即 pip 对应的python是那个版本呢？which python 看看.
    root@iZ2zefl9xsei39b00juvmoZ:/usr/local/bin# which python
    /usr/bin/python

    2. virtualenvwrapper环境，他的bin在哪里呢？可以通过 which virtualenv 查看，因为他俩安装一个bin下.
    root@iZ2zefl9xsei39b00juvmoZ:/usr/local/bin# which virtualenv
    /usr/local/bin/virtualenv

    前往 cd /usr/local/bin/ 进行查看，发现有 virtualenvwrapper.sh 文件，OK。

    3. 需要有一个目录(自定义-WORKON_HOME)，来统一管理所有的虚拟环境
    mkdir /opt/venv

# 第二步，添加环境变量，加到文件尾部
vim /etc/profile
"""
# virtualenvwrapper profile by andy self
export WORKON_HOME=/opt/venv
export VIRTUALENVWRAPPER_PYTHON=/usr/bin/python
source /usr/local/bin/virtualenvwrapper.sh
"""

# 第三步，给virtualenv(which virtualenv)做个软连接(这样，系统命令就有了：virtualenv, 可直接使用)
ln -sf /usr/local/bin/virtualenv /bin/virtualenv

# 查看，软链接创建ok
root@iZ2zefl9xsei39b00juvmoZ:/bin# ls -rtl | grep virtual
lrwxrwxrwx 1 root root      25 Feb 27 22:02 virtualenv -> /usr/local/bin/virtualenv

# 第四步，加载新的/etc/profile环境变量，这样之前的配置才会生效
方法1(需要重新进入root)：
    exit
    sudo su -

方法2：
    执行命令：source /etc/profile

---
再次进入root，可以测试下，使用ok
root@iZ2zefl9xsei39b00juvmoZ:~# workon
test_py366
```

##### 使用

```bash
------------ 创建 ------------
# 创建默认python(python -V)版本的虚拟环境
mkvirtualenv --no-site-packages default_py

# 创建指定某个版本python的环境(如：上边安装的python3.7.0)
mkvirtualenv -p /usr/local/python370/bin/python3 --no-site-packages tt_py370

# 参数说明：
-p                          指定python版本(会复制一份，作为目录(文件夹), 成为虚拟环境目录)
--no-site-packages          即干净的环境，只需必要的包：pip, setuptools, wheel

------------ 常用 ------------
workon                              查看列表
workon [xxname]                     进入xxname环境
deactivate                          退出xxname环境
rmvirtualenv [xxname]               删除xxname环境
```
