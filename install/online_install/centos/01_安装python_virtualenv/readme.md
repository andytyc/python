<!--ts-->

- [准备](#准备)
- [安装 python](#安装-python)
- [更新 pip 国内源](#更新-pip-国内源)
- [venv 安装虚拟环境](#venv-安装虚拟环境)
- [再次安装其他版本 python](#再次安装其他版本-python)

<!-- Added by: edy, at: 2023年 2月 3日 星期五 11时38分11秒 CST -->

<!--te-->

# 准备

工作机器

- 初始化-centos 系统-安装包

```bash
# 修改本地时区
cp -rf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime

# 安装epel yum源
yum -y install epel-release

# 安装各类依赖环境，依赖包 &&& 一般 "初始化centos" 时，都会给centos安装一些必要的环境和包
yum -y groupinstall "Development Tools"
yum -y install openssl-devel bzip2-devel expat-devel gdbm-devel readline-devel sqlite-devel
yum -y install zlib zlib-devel  python-devel  zlib-devel openssl-devel  gcc mysql-devel

# 至此centos系统的初始化使用的安装，全部完成。
```

# 安装 python

```bash
# 下载Python 3.6.6
wget -c https://www.python.org/ftp/python/3.6.6/Python-3.6.6.tar.xz

# 解压编译
tar -xvf Python-3.6.6.tar.xz
cd Python-3.6.6/
./configure --prefix=/usr/local/python366 && make && make install

# 安装3.7报错：
错误: ModuleNotFoundError: No module named '_ctypes'
解决: yum install libffi-devel -y  (3.7以后需要,额外安装此包)

# 验证安装，打印版本
/usr/local/python366/bin/python3 -V
>> Python 3.6.6

# 至此python3.6.6的安装，全部完成。
```

# 更新 pip 国内源

```bash
# 修改pip源为国内源，目的为 pip install 加快速度
mkdir /root/.pip/
vim /root/.pip/pip.conf
"""
[global]
trusted-host=mirrors.aliyun.com
index-url=http://mirrors.aliyun.com/pypi/simple/
"""

# 更新pip
/usr/local/python366/bin/pip3 install --upgrade pip
```

# venv 安装虚拟环境

```bash
# pip安装虚拟环境
/usr/local/python366/bin/pip3 install virtualenvwrapper

# 创建虚拟环境目录(管理所有虚拟环境)
mkdir /opt/venv

# 添加环境变量，加到文件尾部
vim /etc/profile
"""
export WORKON_HOME=/opt/venv
export VIRTUALENVWRAPPER_PYTHON=/usr/local/python366/bin/python3
source /usr/local/python366/bin/virtualenvwrapper.sh
"""

# 给virtualenv做个软连接(这样，系统命令就有了：virtualenv，可直接使用)
ln -sf /usr/local/python366/bin/virtualenv /bin/virtualenv

# 列出虚拟环境列表
workon

# 创建虚拟环境
mkvirtualenv -p /usr/local/python366/bin/python --no-site-packages cmdb366

# 离开虚拟环境
deactivate

# 至此pip源更新和虚拟环境venv，全部完成。
```

# 再次安装其他版本 python

大同小异，参考即可

```bash
# 假如，现在没有python3.6.6，我们来安装一个
# 下载Python 3.6.6
wget -c https://www.python.org/ftp/python/3.6.6/Python-3.6.6.tar.xz

# 解压编译
tar -xvf Python-3.6.6.tar.xz
cd Python-3.6.6/
# 注意，再次安装其他版本(多版本)python时，这里是altinstall,不是install(否则会报错)
./configure --prefix=/usr/local/python366 && make && make altinstall

# 验证安装，打印版本
/usr/local/python366/bin/python3.6 -V
>> Python 3.6.6
```
