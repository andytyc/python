<!--ts-->

- [介绍](#介绍)
- [背景、目标](#背景目标)
- [1. 安装 setuptools](#1-安装-setuptools)
- [2. 安装 pip3](#2-安装-pip3)
- [参考](#参考)

<!-- Added by: edy, at: 2023年 2月 3日 星期五 11时31分05秒 CST -->

<!--te-->

# 介绍

离线安装

- 无法链接外网(如：只能连接自己公司的内网)，或者上不了网(没网)。

- 目的：

  - 安装 python3 任意多个版本;
  - 并安装每个版本的 pip, setuptools, wheel 包;
  - 并创建相应的虚拟环境。

- 注意事项
  - 这里说一下，若系统`自带的python3.6可别乱删`，一般会开机都开不起！这里以血的教训来警告一下大家！
    - 我感觉，以前 python2 不允许删除的原因：系统可能有部分使用着 python2。
    - 但由于 python2 已经开始不更新迭代了，所以估计过渡阶段，部分 python3 自带，并系统也开始使用 python3。
    - 这样估计在几个版本后，可能系统中 python2 就不自带了，观望中。。
  - 至于 ubuntu 从哪个版本开始，开始自带 python3，这个有时间查查。

# 背景、目标

```bash
# 背景(当前服务器)：
1. Ubuntu  18.04 64位, 进入服务器后，发现 python -V为Python 2.7.17，python3 -V 为Python 3.6.9
2. 通过 which python 和 which python3 ，发现 /usr/bin/python 和 /usr/bin/python3 。
3. 通过 pip -V 找到python2的安装位置：pip 9.0.1 from /usr/lib/python2.7/dist-packages (python 2.7)
4. 但在 /usr/lib/ 里虽然有 python3.6 ，但里边没有 dist-packages ，个人认为应该是pip 还没有安装，所以没有任何包(纯净的)。

# 所以这时，我们想安装一个 python3.7.0 的版本，最好创建一个虚拟环境 test_python370 ，用于管理、部署自己的项目。那么，我们在 python3.6 有的情况下，离线安装虚拟包，然后离线安装 python3.7.0，并创建此版本虚拟环境。
```

# 1. 安装 setuptools

安装 pip3 前，必须先安装 setuptools

```bash
# 下载获取setuptools安装包

# 方法1：
    1. 前往：https://pypi.org/project/setuptools/#files 下载setuptools安装包(xxx.zip)。
    2. scp上传(或者使用zlib)至云端服务器，使用 unzip xxx.zip 获取安装包；

# 方法2(采用)：
通过wget下载 setuptools 源码安装包
wget https://pypi.python.org/packages/source/s/setuptools/setuptools-19.6.tar.gz

# 解压
tar -xvf setuptools-19.6.tar.gz

# 切至目录下
cd setuptools-19.6/

# 编译(注意：这里是为python3-->>python3.6.9进行安装setuptools)
python3 setup.py build

# 报错：
Traceback (most recent call last):
  File "setup.py", line 16, in <module>
    from distutils.util import convert_path
ModuleNotFoundError: No module named 'distutils.util'

# 解决，安装python3-distutils：
sudo apt-get install python3-distutils

# 再次编译(成功)
python3 setup.py build

# 安装
python3 setup.py install

# 成功完毕，提示：
... ...
Installed /usr/local/lib/python3.6/dist-packages/setuptools-19.6-py3.6.egg
Processing dependencies for setuptools==19.6
Finished processing dependencies for setuptools==19.6

#############################################

# 注意，网上有种办法，是：
    1. 即下载 setuptools-19.6.tar.gz, 也下载 xxx.zip 俩包；
    2. 然后解压 xxx.tar.gz包后，把xxx.zip文件移到文件夹内；
    3. 运行：python setup.py install 即安装setuptools完毕;
    4. 是否可行，还没试一试。
```

# 2. 安装 pip3

安装 pip3 前，必须先安装 setuptools

```bash
# 通过wget下载pip安装包
wget --no-check-certificate  https://pypi.python.org/packages/source/p/pip/pip-8.0.2.tar.gz#md5=3a73c4188f8dbad6a1e6f6d44d117eeb

# 解压
tar -zxvf pip-8.0.2.tar.gz

# 切目录
cd pip-8.0.2

# 编译
python3 setup.py build

# 安装
python3 setup.py install

# 成功，提示信息：
...
Installed /usr/local/lib/python3.6/dist-packages/pip-8.0.2-py3.6.egg
Processing dependencies for pip==8.0.2
Finished processing dependencies for pip==8.0.2

#############################################

# 查看版本
>> pip3 -V
pip 8.0.2 from /usr/local/lib/python3.6/dist-packages/pip-8.0.2-py3.6.egg (python 3.6)

# 查看目前已安装包
>> pip3 list
certifi (2018.1.18)
chardet (3.0.4)
command-not-found (0.3)
distro-info (0.18ubuntu0.18.04.1)
idna (2.6)
language-selector (0.1)
netifaces (0.10.4)
pip (8.0.2)
pygobject (3.26.1)
python-apt (1.6.4)
PyYAML (3.12)
requests (2.18.4)
setuptools (19.6)
six (1.11.0)
ssh-import-id (5.7)
ufw (0.36)
urllib3 (1.22)

You are using pip version 8.0.2, however version 20.0.2 is available.
You should consider upgrading via the 'pip install --upgrade pip' command.
```

# 参考

- 为 python3.6 安装 pip3
- [安装 zip](https://blog.csdn.net/n_fly/article/details/88368649)

- 方案 1：
  - [下载 setuptools](https://pypi.org/project/setuptools/#files)
  - [为 python3.6 安装 setuptools](https://blog.csdn.net/chenzeze0707/article/details/91344729)
- 方案 2：

  - [阿里云-ECS 服务器-安装 pip3](https://blog.csdn.net/xingzishuai/article/details/84064724)
  - [关于-ubuntu 离线安装软件包-ubuntu 源改为阿里源](https://www.cnblogs.com/xiao987334176/p/9875480.html)

- [其他-下载列表-get-pip3 脚本-virtualenv-看看这个 vir 干什么的](https://bootstrap.pypa.io/)
