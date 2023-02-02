<!--ts-->

- [背景](#背景)
- [Mac](#mac)
  - [自带 python2 安装检查](#自带-python2-安装检查)
  - [自带 python3 安装检查](#自带-python3-安装检查)
  - [自己安装 python3](#自己安装-python3)
    - [homebrew 安装](#homebrew-安装)
    - [手动离线下载安装](#手动离线下载安装)
  - [python 多版本管理工具.pyenv.{重点}](#python-多版本管理工具pyenv重点)
    - [安装](#安装)
    - [使用](#使用)
    - [总结](#总结)
  - [虚拟环境](#虚拟环境)
    - [安装](#安装-1)
    - [总结](#总结-1)

<!-- Added by: edy, at: 2022年 2月15日 星期二 10时59分25秒 CST -->

<!--te-->

# 背景

`linux,mac,windows`系统都会自带 python，系统版本是最新的 v2.x.x。

```bash
# 进入python在终端的交互模式
python

# 可以看到版本2.x, 退出此模式
exit()

# 可以查看版本, 相关支持命令：python --help
python --version
# 或
python -V
# 查看可执行命令位置, 若没有可以从安装目录的bin目录下，将python命令创建软链接到任意指定位置
which python
# 或
where python

# 查看pip版本
pip --version
# 或
pip -V
# 查看可执行命令位置, 若没有可以从安装目录的bin目录下，将pip命令创建软链接到任意指定位置
which pip
# 或
where pip
```

# Mac

这台电脑是刚把之前的换了台，但也是之前有人用过的，先查看系统中目前的 python 环境怎样

```bash
# edy@edydeMacBook-Pro ipython % which python
/usr/bin/python
# edy@edydeMacBook-Pro ipython % which pip
pip not found
# edy@edydeMacBook-Pro ipython % pip -V
zsh: command not found: pip
# edy@edydeMacBook-Pro ipython % python -V
Python 2.7.16
# edy@edydeMacBook-Pro ipython % which python3
/usr/bin/python3
# edy@edydeMacBook-Pro ipython % which pip3
/usr/bin/pip3
# edy@edydeMacBook-Pro ipython % pip3 -V
pip 19.2.3 from /Library/Developer/CommandLineTools/Library/Frameworks/Python3.framework/Versions/3.8/lib/python3.8/site-packages/pip (python 3.8)
# edy@edydeMacBook-Pro ipython % python3 -V
Python 3.8.2
```

可以发现 python3 竟然也存在，看起来有点混乱，查看下具体情况

```bash
# edy@edydeMacBook-Pro ipython % cd /usr/bin
# edy@edydeMacBook-Pro bin % ls -rtli | grep python
1152921500311879999 -rwxr-xr-x   1 root   wheel     31488  8 11  2020 python3
1152921500311880101 lrwxr-xr-x   1 root   wheel        75  9 23 13:54 python -> ../../System/Library/Frameworks/Python.framework/Versions/2.7/bin/python2.7
1152921500311880108 lrwxr-xr-x   1 root   wheel        75  9 23 13:54 python2 -> ../../System/Library/Frameworks/Python.framework/Versions/2.7/bin/python2.7
1152921500311880117 lrwxr-xr-x   1 root   wheel        76  9 23 13:54 pythonw -> ../../System/Library/Frameworks/Python.framework/Versions/2.7/bin/pythonw2.7
1152921500311880192 lrwxr-xr-x   1 root   wheel        82  9 23 13:54 python2.7-config -> ../../System/Library/Frameworks/Python.framework/Versions/2.7/bin/python2.7-config
1152921500311880424 lrwxr-xr-x   1 root   wheel        76  9 23 13:54 pythonw2.7 -> ../../System/Library/Frameworks/Python.framework/Versions/2.7/bin/pythonw2.7
1152921500311880551 lrwxr-xr-x   1 root   wheel        82  9 23 13:54 python-config -> ../../System/Library/Frameworks/Python.framework/Versions/2.7/bin/python2.7-config
1152921500311880926 lrwxr-xr-x   1 root   wheel        75  9 23 13:54 python2.7 -> ../../System/Library/Frameworks/Python.framework/Versions/2.7/bin/python2.7
# edy@edydeMacBook-Pro bin % ls -rtli | grep pip
1152921500311880137 -rwxr-xr-x   1 root   wheel     31488  8 11  2020 pip3
# edy@edydeMacBook-Pro bin % ls -rtli | grep easy_install
1152921500311880091 -rwxr-xr-x   2 root   wheel       544  6  6  2020 easy_install-2.7
1152921500311880091 -rwxr-xr-x   2 root   wheel       544  6  6  2020 easy_install
```

可以发现对于 python2 版本是有着正常的软连接的，但是 pip 并不存在 bin 中，导致无法直接使用。另外，`python3,pip3`不是软链接而是真实命令文件，来看下各自具体安装目录情况。

而 easy_install 通过文件号`1152921500311880091`是一样的，可以知道这俩文件是同一个。

## 自带 python2 安装检查

```bash
# edy@edydeMacBook-Pro bin % cd ../../System/Library/Frameworks/Python.framework/Versions/2.7
# edy@edydeMacBook-Pro 2.7 % cd bin
edy@edydeMacBook-Pro bin % ls
2to3                    idle2                   python                  python2.7-config        smtpd2.7.py
2to3-2                  idle2.7                 python-config           pythonw                 smtpd2.py
2to3-2.7                pydoc                   python2                 pythonw2
2to32.7                 pydoc2                  python2-config          pythonw2.7
idle                    pydoc2.7                python2.7               smtpd.py
# edy@edydeMacBook-Pro bin % ls -rtli | grep python
1152921500312160356 -rwxr-xr-x  1 root  wheel   1842  6  6  2020 python2.7-config
1152921500312160365 -rwxr-xr-x  1 root  wheel  31728  8 11  2020 python2.7
1152921500312160360 -rwxr-xr-x  1 root  wheel  31728  8 11  2020 pythonw2.7
1152921500312160349 lrwxr-xr-x  1 root  wheel     16  9 23 13:58 python2-config -> python2.7-config
1152921500312160353 lrwxr-xr-x  1 root  wheel      7  9 23 13:58 python -> python2
1152921500312160354 lrwxr-xr-x  1 root  wheel      9  9 23 13:58 python2 -> python2.7
1152921500312160355 lrwxr-xr-x  1 root  wheel      8  9 23 13:58 pythonw -> pythonw2
1152921500312160362 lrwxr-xr-x  1 root  wheel     14  9 23 13:58 python-config -> python2-config
1152921500312160363 lrwxr-xr-x  1 root  wheel     10  9 23 13:58 pythonw2 -> pythonw2.7
# 可以发现，python是python2的软链接，python2是python2.7的软链接, 所以如果以后外边的bin创建软链接时也用python2.7就可以

# 看看lib里有没有site-packages
# edy@edydeMacBook-Pro python2.7 % ls | grep site-packages
```

可以发现，bin 里没有 pip，并且 lib/python2.7 里没有 site-packages 目录，正常 site-packages 目录里有 pip。
官方给的方法是，通过 easy_install 可以直接安装 pip

```bash
# edy@edydeMacBook-Pro bin % sudo easy_install pip
Password:
Searching for pip
Reading https://pypi.org/simple/pip/
Downloading https://files.pythonhosted.org/packages/88/d9/761f0b1e0551a3559afe4d34bd9bf68fc8de3292363b3775dda39b62ce84/pip-22.0.3.tar.gz#sha256=f29d589df8c8ab99c060e68ad294c4a9ed896624f6368c5349d70aa581b333d0
Best match: pip 22.0.3
Processing pip-22.0.3.tar.gz
Writing /tmp/easy_install-_kswk8/pip-22.0.3/setup.cfg
Running pip-22.0.3/setup.py -q bdist_egg --dist-dir /tmp/easy_install-_kswk8/pip-22.0.3/egg-dist-tmp-8gt54o
Traceback (most recent call last):
  File "/usr/bin/easy_install", line 13, in <module>
    load_entry_point('setuptools==41.0.1', 'console_scripts', 'easy_install')()
  File "/System/Library/Frameworks/Python.framework/Versions/2.7/Extras/lib/python/setuptools/command/easy_install.py", line 2316, in main
    **kw
  File "/System/Library/Frameworks/Python.framework/Versions/2.7/Extras/lib/python/setuptools/__init__.py", line 145, in setup
    return distutils.core.setup(**attrs)
  File "/System/Library/Frameworks/Python.framework/Versions/2.7/lib/python2.7/distutils/core.py", line 151, in setup
    dist.run_commands()
  File "/System/Library/Frameworks/Python.framework/Versions/2.7/lib/python2.7/distutils/dist.py", line 953, in run_commands
    self.run_command(cmd)
  File "/System/Library/Frameworks/Python.framework/Versions/2.7/lib/python2.7/distutils/dist.py", line 972, in run_command
    cmd_obj.run()
  File "/System/Library/Frameworks/Python.framework/Versions/2.7/Extras/lib/python/setuptools/command/easy_install.py", line 418, in run
    self.easy_install(spec, not self.no_deps)
  File "/System/Library/Frameworks/Python.framework/Versions/2.7/Extras/lib/python/setuptools/command/easy_install.py", line 679, in easy_install
    return self.install_item(spec, dist.location, tmpdir, deps)
  File "/System/Library/Frameworks/Python.framework/Versions/2.7/Extras/lib/python/setuptools/command/easy_install.py", line 705, in install_item
    dists = self.install_eggs(spec, download, tmpdir)
  File "/System/Library/Frameworks/Python.framework/Versions/2.7/Extras/lib/python/setuptools/command/easy_install.py", line 890, in install_eggs
    return self.build_and_install(setup_script, setup_base)
  File "/System/Library/Frameworks/Python.framework/Versions/2.7/Extras/lib/python/setuptools/command/easy_install.py", line 1158, in build_and_install
    self.run_setup(setup_script, setup_base, args)
  File "/System/Library/Frameworks/Python.framework/Versions/2.7/Extras/lib/python/setuptools/command/easy_install.py", line 1144, in run_setup
    run_setup(setup_script, args)
  File "/System/Library/Frameworks/Python.framework/Versions/2.7/Extras/lib/python/setuptools/sandbox.py", line 253, in run_setup
    raise
  File "/System/Library/Frameworks/Python.framework/Versions/2.7/lib/python2.7/contextlib.py", line 35, in __exit__
    self.gen.throw(type, value, traceback)
  File "/System/Library/Frameworks/Python.framework/Versions/2.7/Extras/lib/python/setuptools/sandbox.py", line 195, in setup_context
    yield
  File "/System/Library/Frameworks/Python.framework/Versions/2.7/lib/python2.7/contextlib.py", line 35, in __exit__
    self.gen.throw(type, value, traceback)
  File "/System/Library/Frameworks/Python.framework/Versions/2.7/Extras/lib/python/setuptools/sandbox.py", line 166, in save_modules
    saved_exc.resume()
  File "/System/Library/Frameworks/Python.framework/Versions/2.7/Extras/lib/python/setuptools/sandbox.py", line 141, in resume
    six.reraise(type, exc, self._tb)
  File "/System/Library/Frameworks/Python.framework/Versions/2.7/Extras/lib/python/setuptools/sandbox.py", line 154, in save_modules
    yield saved
  File "/System/Library/Frameworks/Python.framework/Versions/2.7/Extras/lib/python/setuptools/sandbox.py", line 195, in setup_context
    yield
  File "/System/Library/Frameworks/Python.framework/Versions/2.7/Extras/lib/python/setuptools/sandbox.py", line 250, in run_setup
    _execfile(setup_script, ns)
  File "/System/Library/Frameworks/Python.framework/Versions/2.7/Extras/lib/python/setuptools/sandbox.py", line 44, in _execfile
    code = compile(script, filename, 'exec')
  File "/tmp/easy_install-_kswk8/pip-22.0.3/setup.py", line 7
    def read(rel_path: str) -> str:
                     ^
SyntaxError: invalid syntax
```

结果安装失败了，有一个语法错误。进行解决，使用官方给的另一个安装 pip 方式。

```bash
# 下载 get-pip.py 脚本文件
# curl 'https://bootstrap.pypa.io/get-pip.py' > get-pip.py

# edy@edydeMacBook-Pro ~ % cd chuyt/download
# edy@edydeMacBook-Pro download % ls
# edy@edydeMacBook-Pro download % curl 'https://bootstrap.pypa.io/get-pip.py' > get-pip.py
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100 2548k  100 2548k    0     0   477k      0  0:00:05  0:00:05 --:--:--  512k
# edy@edydeMacBook-Pro download % ls
get-pip.py

# 安装python2对应的pip
# edy@edydeMacBook-Pro download % sudo python get-pip.py
Password:
ERROR: This script does not work on Python 2.7 The minimum supported Python version is 3.7. Please use https://bootstrap.pypa.io/pip/2.7/get-pip.py instead.

# 发现这个版本不支持python2.x，需要下载另一个版本，也就是提示的网址
# curl 'https://bootstrap.pypa.io/pip/2.7/get-pip.py' > get-pip-2.7.py

# edy@edydeMacBook-Pro download % curl 'https://bootstrap.pypa.io/pip/2.7/get-pip.py' > get-pip-2.7.py

  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100 1863k  100 1863k    0     0  1035k      0  0:00:01  0:00:01 --:--:-- 1035k
# edy@edydeMacBook-Pro download % ls
get-pip-2.7.py  get-pip.py

# 安装python2对应的pip
# edy@edydeMacBook-Pro download % sudo python get-pip-2.7.py
DEPRECATION: Python 2.7 reached the end of its life on January 1st, 2020. Please upgrade your Python as Python 2.7 is no longer maintained. pip 21.0 will drop support for Python 2.7 in January 2021. More details about Python 2 support in pip can be found at https://pip.pypa.io/en/latest/development/release-process/#python-2-support pip 21.0 will remove support for this functionality.
WARNING: The directory /Users/edy/Library/Caches/pip or its parent directory is not owned or is not writable by the current user. The cache has been disabled. Check the permissions and owner of that directory. If executing pip with sudo, you may want sudo is -H flag.
Collecting pip<21.0
  Downloading pip-20.3.4-py2.py3-none-any.whl (1.5 MB)
     |████████████████████████████████| 1.5 MB 514 kB/s
Installing collected packages: pip
Successfully installed pip-20.3.4

# 安装成功了，来查看pip
# edy@edydeMacBook-Pro download % pip -V
pip 20.3.4 from /Library/Python/2.7/site-packages/pip (python 2.7)
# edy@edydeMacBook-Pro download % which pip
/usr/local/bin/pip
# edy@edydeMacBook-Pro download % pip2 -V
pip 20.3.4 from /Library/Python/2.7/site-packages/pip (python 2.7)
# edy@edydeMacBook-Pro download % which pip2
/usr/local/bin/pip2

# pip命令在 /usr/local/bin 中

# 注意: pip的site-packages没在上边python所在目录里，而是在pip -V显示的目录里
# edy@edydeMacBook-Pro bin % cd /Library/Python/2.7
# edy@edydeMacBook-Pro site-packages % ls
Extras.pth              README                  pip                     pip-20.3.4.dist-info
# 所以，以后的pip安装依赖包都会在这个目录下/Library/Python/2.7/site-packages。

# 查看pip情况
# edy@edydeMacBook-Pro ipython % cd /usr/local/bin
# edy@edydeMacBook-Pro bin % ls -rtli | grep pip
12891345495 -rwxr-xr-x  1 root  admin     304  2 14 11:54 pip
12891345496 -rwxr-xr-x  1 root  admin     304  2 14 11:54 pip2
12891345497 -rwxr-xr-x  1 root  admin     304  2 14 11:54 pip2.7

# 如果以后想卸载pip，执行卸载命令就可以
sudo pip uninstall pip
```

到此为止可以发现目前的 python2 环境是干净的了，虽然 pip 和 python 分别在/usr/local/bin 和/usr/bin 中，但都在环境变量中可以直接使用。

```bash
# edy@edydeMacBook-Pro ipython % python -V
Python 2.7.16
# edy@edydeMacBook-Pro ipython % pip -V
pip 20.3.4 from /Library/Python/2.7/site-packages/pip (python 2.7)
# edy@edydeMacBook-Pro ipython % python2 -V
Python 2.7.16
# edy@edydeMacBook-Pro ipython % pip2 -V
pip 20.3.4 from /Library/Python/2.7/site-packages/pip (python 2.7)
# edy@edydeMacBook-Pro ipython % which python python2 pip pip2
/usr/bin/python
/usr/bin/python2
/usr/local/bin/pip
/usr/local/bin/pip2
```

## 自带 python3 安装检查

然后，来看看目前已经有的 python3 的安装目录情况

```bash
# edy@edydeMacBook-Pro bin % pip3 -V
pip 19.2.3 from /Library/Developer/CommandLineTools/Library/Frameworks/Python3.framework/Versions/3.8/lib/python3.8/site-packages/pip (python 3.8)

# pip3 -V 知道了pip3安装目录，来到上级的bin发现确实就是在python3的安装目录下
# edy@edydeMacBook-Pro 3.8 % cd /Library/Developer/CommandLineTools/Library/Frameworks/Python3.framework/Versions/3.8
# edy@edydeMacBook-Pro 3.8 % ls
Headers         Python3         Resources       _CodeSignature  bin             include         lib             share
# edy@edydeMacBook-Pro 3.8 % cd bin
# edy@edydeMacBook-Pro bin % ls
2to3            2to3-3.8        pydoc3          pydoc3.8        python3         python3.8
# edy@edydeMacBook-Pro bin % ./python3

# 查看文件信息
# edy@edydeMacBook-Pro bin % ls -rtli | grep python
12884977190 -rwxr-xr-x  1 root  wheel  151120  1  9  2021 python3.8
12884977189 lrwxr-xr-x  1 root  wheel       9  9 29 13:06 python3 -> python3.8
```

python3 是 python3.8 的软链接, 这里我们直接做软链接替换了之前 /usr/bin/python3, 保证文件的一致性，看大小不一致谁知道之前的 python3 怎么来的？所以替换了。

```bash
# edy@edydeMacBook-Pro bin % sudo mv python3 python3-old
Password:
mv: rename python3 to python3-old: Operation not permitted
# edy@edydeMacBook-Pro bin % sudo rm -rf python3
rm: python3: Operation not permitted
# edy@edydeMacBook-Pro bin % chmod 777 /usr/bin
chmod: Unable to change file mode on /usr/bin: Operation not permitted

# 这个问题解决方案见: issue/problems/01
# 解决后，将SIP保护机制再开启来。

# edy@edydeMacBook-Pro bin % pwd
/usr/bin
# edy@edydeMacBook-Pro bin % sudo ln -sf /Library/Developer/CommandLineTools/Library/Frameworks/Python3.framework/Versions/3.8/bin/python3.8 /usr/bin/python3
Password:
# edy@edydeMacBook-Pro bin % ls -rtli | grep python3
1152921500311879999 -rwxr-xr-x   1 root   wheel     31488  8 11  2020 python3-old
1152921500312401675 lrwxr-xr-x   1 root   wheel        99  2 14 14:00 python3 -> /Library/Developer/CommandLineTools/Library/Frameworks/Python3.framework/Versions/3.8/bin/python3.8
```

到此为止 python3 的环境也已经摸清了。

```bash
# edy@edydeMacBook-Pro ipython % pip3 -V
pip 19.2.3 from /Library/Developer/CommandLineTools/Library/Frameworks/Python3.framework/Versions/3.8/lib/python3.8/site-packages/pip (python 3.8)
# edy@edydeMacBook-Pro ipython % which pip3
/usr/bin/pip3
# edy@edydeMacBook-Pro ipython % which python3
/usr/bin/python3
# edy@edydeMacBook-Pro ipython % python3 -V
Python 3.8.2
```

## 自己安装 python3

### homebrew 安装

1. 安装 homebrew

已经安装的跳过

```bash
# /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
==> Installation successful!

==> Homebrew has enabled anonymous aggregate user behaviour analytics.
Read the analytics documentation (and how to opt-out) here:
  https://docs.brew.sh/Analytics.html

==> Next steps:
- Run `brew help` to get started
- Further documentation:
    https://docs.brew.sh
```

2. 安装 python

mac 自带 python 为 python2 版本，对应 pip。计划安装 python3，对应 pip3。

安装 python3

```bash
# edy@edydeMacBook-Pro ~ % brew install python3
# 一开始报错了，是因为homebrew之前安装的有问题，解决方法见:issue/problems/02
# 没有错误后，开始执行安装python3即可。

# edy@edydeMacBook-Pro ~ % brew install python3
Updating Homebrew...
==> Auto-updated Homebrew!
Updated 3 taps (homebrew/core, homebrew/services and mongodb/brew).
==> New Formulae
... ...
==> Caveats
==> python@3.9
Python has been installed as
  /usr/local/bin/python3

Unversioned symlinks `python`, `python-config`, `pip` etc. pointing to
`python3`, `python3-config`, `pip3` etc., respectively, have been installed into
  /usr/local/opt/python@3.9/libexec/bin

You can install Python packages with
  pip3 install <package>
They will install into the site-package directory
  /usr/local/lib/python3.9/site-packages

tkinter is no longer included with this formula, but it is available separately:
  brew install python-tk@3.9

See: https://docs.brew.sh/Homebrew-and-Python
==> redis
To restart redis after an upgrade:
  brew services restart redis
Or, if you don not want/need a background service you can just run:
  /usr/local/opt/redis/bin/redis-server /usr/local/etc/redis.conf
```

安装完毕后，查看当前系统的 python3 被谁指向，还是之前的`v3.8.2`吗？答案：`不是`。

来看看目前系统的 python2,python3 情况

```bash
# 看看pip
# edy@edydeMacBook-Pro bin % which pip3
/usr/local/bin/pip3
# edy@edydeMacBook-Pro bin % which pip2
/usr/local/bin/pip2
# edy@edydeMacBook-Pro bin % which pip
/usr/local/bin/pip
# edy@edydeMacBook-Pro bin % cd /usr/local/bin
# edy@edydeMacBook-Pro bin % ls -rtli | grep pip
12891345495 -rwxr-xr-x  1 root  admin     304  2 14 11:54 pip
12891345496 -rwxr-xr-x  1 root  admin     304  2 14 11:54 pip2
12891345497 -rwxr-xr-x  1 root  admin     304  2 14 11:54 pip2.7
12891402348 lrwxr-xr-x  1 edy   admin      36  2 14 14:54 pip3 -> ../Cellar/python@3.9/3.9.10/bin/pip3
12891402350 lrwxr-xr-x  1 edy   admin      38  2 14 14:54 pip3.9 -> ../Cellar/python@3.9/3.9.10/bin/pip3.9

# 看看python
# edy@edydeMacBook-Pro bin % which python3
/usr/local/bin/python3
# edy@edydeMacBook-Pro bin % which python
/usr/bin/python
# edy@edydeMacBook-Pro bin % which python2
/usr/bin/python2
# edy@edydeMacBook-Pro bin % cd /usr/local/bin
# edy@edydeMacBook-Pro bin % ls -rtli | grep python
12891399431 lrwxr-xr-x  1 edy   admin      36  2 14 14:54 2to3 -> ../Cellar/python@3.9/3.9.10/bin/2to3
12891399432 lrwxr-xr-x  1 edy   admin      40  2 14 14:54 2to3-3.9 -> ../Cellar/python@3.9/3.9.10/bin/2to3-3.9
12891399433 lrwxr-xr-x  1 edy   admin      37  2 14 14:54 idle3 -> ../Cellar/python@3.9/3.9.10/bin/idle3
12891399434 lrwxr-xr-x  1 edy   admin      39  2 14 14:54 idle3.9 -> ../Cellar/python@3.9/3.9.10/bin/idle3.9
12891399435 lrwxr-xr-x  1 edy   admin      38  2 14 14:54 pydoc3 -> ../Cellar/python@3.9/3.9.10/bin/pydoc3
12891399436 lrwxr-xr-x  1 edy   admin      40  2 14 14:54 pydoc3.9 -> ../Cellar/python@3.9/3.9.10/bin/pydoc3.9
12891399437 lrwxr-xr-x  1 edy   admin      39  2 14 14:54 python3 -> ../Cellar/python@3.9/3.9.10/bin/python3
12891399438 lrwxr-xr-x  1 edy   admin      46  2 14 14:54 python3-config -> ../Cellar/python@3.9/3.9.10/bin/python3-config
12891399439 lrwxr-xr-x  1 edy   admin      41  2 14 14:54 python3.9 -> ../Cellar/python@3.9/3.9.10/bin/python3.9
12891399440 lrwxr-xr-x  1 edy   admin      48  2 14 14:54 python3.9-config -> ../Cellar/python@3.9/3.9.10/bin/python3.9-config
12891402348 lrwxr-xr-x  1 edy   admin      36  2 14 14:54 pip3 -> ../Cellar/python@3.9/3.9.10/bin/pip3
12891402349 lrwxr-xr-x  1 edy   admin      38  2 14 14:54 wheel3 -> ../Cellar/python@3.9/3.9.10/bin/wheel3
12891402350 lrwxr-xr-x  1 edy   admin      38  2 14 14:54 pip3.9 -> ../Cellar/python@3.9/3.9.10/bin/pip3.9

# 再看看pip(管理安装包的管理器，安装的依赖包都会在这里)目录在哪里
# edy@edydeMacBook-Pro bin % pip -V
pip 20.3.4 from /Library/Python/2.7/site-packages/pip (python 2.7)
# edy@edydeMacBook-Pro bin % pip2 -V
pip 20.3.4 from /Library/Python/2.7/site-packages/pip (python 2.7)
# edy@edydeMacBook-Pro bin % pip3 -V
pip 21.3.1 from /usr/local/lib/python3.9/site-packages/pip (python 3.9)
```

### 手动离线下载安装

```bash
# 官网下载直接安装
```

## python 多版本管理工具.pyenv.{重点}

先看下目前的系统 python 情况，以及目前 python 的安装背景。

```bash
###### pip ######

# edy@edydeMacBook-Pro bin % which pip
/usr/local/bin/pip
# edy@edydeMacBook-Pro bin % which pip3
/usr/local/bin/pip3

# 看看pip具体安装目录在哪里

# edy@edydeMacBook-Pro bin % pip -V
pip 20.3.4 from /Library/Python/2.7/site-packages/pip (python 2.7)
# edy@edydeMacBook-Pro bin % pip3 -V
pip 21.3.1 from /usr/local/lib/python3.9/site-packages/pip (python 3.9)

###### python ######

# edy@edydeMacBook-Pro bin % which python
/usr/bin/python
# edy@edydeMacBook-Pro bin % which python3
/usr/local/bin/python3

# 看看python具体安装目录在哪里

# edy@edydeMacBook-Pro bin % cd /usr/bin
# edy@edydeMacBook-Pro bin % ls -rtli | grep python
1152921500311880101 lrwxr-xr-x   1 root   wheel        75  9 23 13:54 python -> ../../System/Library/Frameworks/Python.framework/Versions/2.7/bin/python2.7

# edy@edydeMacBook-Pro bin % cd /usr/local/bin
# edy@edydeMacBook-Pro bin % ls -rtli | grep python
12891399437 lrwxr-xr-x  1 edy   admin      39  2 14 14:54 python3 -> ../Cellar/python@3.9/3.9.10/bin/python3

###### python安装背景总结 ######

# python2
python存在自带，但没有pip，所以看 自带python2 安装检查 进行的安装

# python3
python3之前有人安装过，先看 自带python2 安装检查 进行检查安装，然后进行了 homebrew 手动安装了python3

# 最后
然后，就是目前的这个局面了。
```

### 安装

通过这些情况可以看出，还是有点点混乱，虽然通过虚拟环境可以生成独立环境，但是假如我们就是需要系统的 python 要有多个版本的时候呢？

> 有时多个项目，生产环境的 python 不同，又不方便升级，进行同时维护时就需要这种场景了。
> 有时，自己在不同版本下测试 python 新的特性和不同之处，也需要。

挺好的解决办法，就是安装一个 python 版本管理工具 pyenv

```bash
# mac上安装多个Python版本，使用pyenv来管理多个Python版本

# 自己的笔记
# https://blog.csdn.net/weixin_41957017/article/details/84644635

# 是否安装
# edy@edydeMacBook-Pro ~ % pyenv -v
zsh: command not found: pyenv

# 安装
# edy@edydeMacBook-Pro ~ % brew install pyenv
... ...
==> Installing pyenv
==> Pouring pyenv-2.2.4-1.catalina.bottle.tar.gz
🍺  /usr/local/Cellar/pyenv/2.2.4-1: 859 files, 2.8MB

# 是否安装
# edy@edydeMacBook-Pro ~ % pyenv -v
pyenv 2.2.4
```

### 使用

```bash
# 查看所有的已安装的python版本（pyenv管理的所有版本）
edy@edydeMacBook-Pro ~ % pyenv versions
# * system (set by /Users/edy/.pyenv/version)  # * 表示当前正在使用的版本，system表示用的是系统python版本

# 查看可以安装的python版本
$ pyenv install --list
'''
Available versions:
  2.1.3
  2.2.3
  2.3.7
  ...
'''

# 选择版本进行安装
$ pyenv install 3.5.5
'''
python-build: use openssl from homebrew
python-build: use readline from homebrew
Downloading Python-3.5.5.tar.xz...
-> https://www.python.org/ftp/python/3.5.5/Python-3.5.5.tar.xz
Installing Python-3.5.5...
python-build: use readline from homebrew
Installed Python-3.5.5 to /Users/xxx/.pyenv/versions/3.5.5
... ...
# 有时，等上一会儿，也能安装成功；
# 有时，会卡在这里（墙内环境），可以开代理，或者使用国内镜像
'''

################### 国内镜像源 ###################

# 方式1，直接终端执行命令：
# 使用国内镜像安装，执行 安装python3.5.5 的命令(注意安装过程中python-build: 会有段时间大概3~5分钟吧，就差不多了)：
# 搜狐(不能用了403)
v=3.5.5 && wget http://mirrors.sohu.com/python/$v/Python-$v.tar.xz -P ~/.pyenv/cache/ && pyenv install $v
# 淘宝
v=3.5.5 && wget http://npm.taobao.org/mirrors/python/$v/Python-$v.tar.xz -P ~/.pyenv/cache/ && pyenv install $v
# 参考:
# https://wxnacy.com/2020/09/30/pyenv-install-use-mirrors/

# 若提示, zsh: command not found: wget
# 安装wget即可：brew install wget

# pyenv安装知识：
1. pyenv安装的所有版本的Python都在 ~/.pyenv/versions 目录下，而 ~/.pyenv/shims 是pyenv切换不同版本后指向的bin
2. ~/.pyenv目录，上边只要执行过一次 pyenv install 3.5.5 就会自动生成的。

# 方式2:
# 也可以创建一个方法，放到 linux(~/.bashrc), mac(~/.bash_profile或~/.zshrc) 文件中，以后方便直接使用

vi ~/.zshrc
'''
# python pyenv path
export PYENV_ROOT=~/.pyenv
export PATH=$PYENV_ROOT/shims:$PATH

# python pyenv for install python, ps: pyinstall 3.6.6
function pyinstall() {
    v=$1
    echo '准备按照 Python' $v
    #curl -L https://npm.taobao.org/mirrors/python/$v/Python-$v.tar.xz -o ~/.pyenv/cache/Python-$v.tar.xz
    wget http://npm.taobao.org/mirrors/python/$v/Python-$v.tar.xz -P ~/.pyenv/cache/
    pyenv install $v
}
'''

###################

# 切换版本（全局）
$ pyenv global 3.5.5 # 全局切换
$ python -V # 验证一下是否切换成功

# 切换版本（局部），也可用local，但只对当前目录生效
$ pyenv local 3.5.5 # 当前目录及其目录切换
$ python -V # 验证一下是否切换成功

################# 坑点：（环境变量）#################

# 用pyenv versions查看，明明已经切换成功，但是用 python -V 却还是系统版本。原因是: pyenv没有加到$PATH环境变量 里去，解决办法如下：
export PYENV_ROOT=~/.pyenv
# if which pyenv > /dev/null; then eval "$(pyenv init -)"; fi   # 我不添加，没有问题，如果有位置异常，添加试试，这里意思：pyenv如果找不到时，执行初始化命令
export PATH=$PYENV_ROOT/shims:$PATH

# 环境变量的知识：
# 1. 环境变量可以这么粗暴的理解，它是一个目录路径，在这个目录下有着一些命令名称(如：python,pip)，shell终端会加载进来，从而用户命令使用。
# 2. Mac下环境变量加载顺序：/etc/profile /etc/paths ~/.bash_profile ~/.bash_login ~/.profile ~/.bashrc
## 2.1 首先，/etc/profile /etc/paths，都是系统级别，Mac系统启动就会加载。后面几个是当前用户级的环境变量。
## 2.2 其次，~/.bash_profile ~/.bash_login ~/.profile，按照从前往后的顺序读取，如果~/.bash_profile文件存在，则后面的几个文件就会被忽略不读了，如果~/.bash_profile文件不存在，才会以此类推读取后面的文件。
## 2.3 最终，~/.bashrc，没有上述规则，它是bash shell打开的时候载入的。mac 一般使用bash作为默认shell
# 3. 格式(冒号隔开)：export PATH=$PATH:<PATH 1>:<PATH 2>:<PATH 3>:xxx。提示：输入环境变量时，不用一个一个地输入，只要拖动文件夹到 Terminal 里就可以了。
# 4. 查看当前用户的环境变量，在终端：echo $PATH
# 5. 一般环境变量文件加载，须重启后生效：source ~/.bash_profile (环境变量文件)。

# ~/.bash_profile，为每个用户下的环境变量配置文件，对该用户（不是root哦）安装、使用的所有软件、程序
# $PATH -> 表示当前已有的环境变量
# : -> 冒号，是每个环境变量之间的符号
# export -> shell命令，设置电脑的全局变量

################# 坑点解决：环境变量 #################

# 可以把上边两句命令，加到~/.bash_profile里去，永久生效
vi ~/.bash_profile   # 或其他启动终端环境文件，vi ~/.zshrc
'''
# pyenv path
export PYENV_ROOT=~/.pyenv
export PATH=$PYENV_ROOT/shims:$PATH
'''

# 坑点：
# 以上修改环境变量后，发现还是没切换成功，为什么？
# 因为环境变量没有加载进来，这样两步执行后，就可以了：
source ~/.bash_profile

# 将终端关闭，在开启，就OK了（有时，不需要重新启动终端也行，以后在研究咋回事吧）

# 如果是root的其他情况，需要使用此命令进入root权限，这样会加载一次环境变量
sudo su -

# 这时可以，看看该版本的安装目录：
which python
# 这样，在设置虚拟环境时，就很方便了，可以为不同版本设置不同的Python版本环境使用，贼舒服

# 有时设置了pyenv local版本后，再设置global会发现没有生效，可以尝试：
pyenv local --unset    # 解除local设置

# 可以使用了，如，切换回系统版本：
$ pyevn global system

# 卸载Python版本
$ pyenv uninstall 3.5.5

# 查看pyenv指令列表
$ pyenv commands
```

### 总结

环境变量

> 如 mac 的`vi ~/.zshrc`

```bash
# python pyenv path
export PYENV_ROOT=~/.pyenv
export PATH=$PYENV_ROOT/shims:$PATH

# python pyenv for install python, ps: pyinstall 3.6.6
function pyinstall() {
    v=$1
    echo '准备安装 Python' $v
    #curl -L https://npm.taobao.org/mirrors/python/$v/Python-$v.tar.xz -o ~/.pyenv/cache/Python-$v.tar.xz
    wget http://npm.taobao.org/mirrors/python/$v/Python-$v.tar.xz -P ~/.pyenv/cache/
    pyenv install $v
}
```

安装任意版本的 python，常用命令

```bash
# 查看可安装版本
pyenv install --list

# 已安装的版本(pyenv管理的)
pyenv versions

# 安装指定Python版本
v=3.5.5 && wget http://npm.taobao.org/mirrors/python/$v/Python-$v.tar.xz -P ~/.pyenv/cache/ && pyenv install $v
# 或(建议)
pyinstall 3.5.5

# 卸载指定Python版本
pyenv uninstall 3.5.5

# 切换版本
pyenv global 3.5.5 # 全局切换
pyenv local 3.5.5 # 当前目录及其目录切换
pyenv local --unset # 解除local设置, 否则若当前目录local切了，global在当前目录不生效，需要解除
```

## 虚拟环境

virtualenv，是通过 pip 安装的，所有当前 python 的版本是哪一个，它就通过哪一个版本目录下的 lib 库里安装包 site-packages 安装的。

目的：

这里，使用 virtualenv 以及 pyenv ，实现多个 python 版本的虚拟环境的使用，贼舒服！

区别:

virtualenv：可以用来建立一个专属于项目的 python 环境，保持一个干净的环境。
virtaulenvwrapper：是 virtualenv 的扩展包(是面向 virtualenv 的调用工具)，可以更方便地新增，删除，复制，切换虚拟环境。

### 安装

```bash
# 查看是否安装
virtualenv --version
# zsh: command not found: virtualenv

# 切换python到2.7.x吧，因为安装virtualenv对python版本没什么高要求，2.7.x系统自带不会被其他人无意删除掉。
pyenv global system

# edy@edydeMacBook-Pro ~ % python -V
# Python 2.7.16
# edy@edydeMacBook-Pro ~ % pip -V
# pip 20.3.4 from /Library/Python/2.7/site-packages/pip (python 2.7)

# 安装virtualenv
sudo pip install virtualenv

# 查看是否安装,查看版本
virtualenv --version
# virtualenv 20.13.1 from /Library/Python/2.7/site-packages/virtualenv/__init__.pyc

# 查看安装路径
which virtualenv
# /usr/local/bin/virtualenv

######### 安装virtualenvwrapper #########

# 安装 virtualenvwrapper，来更加方便(快捷键)的使用virtualenv
sudo easy_install virtualenvwrapper
# 或者(建议pip安装), easy_install有语法错误
sudo pip install virtualenvwrapper
# ERROR: Package 'stevedore' requires a different Python: 2.7.16 not in '>=3.6'
# 但报错提示版本需要>=3.6

# 解决:
# 通过python3.6.6来安装(注意：这样一来，等我们配置环境变量时，我们配置的virtualenv是 3.6.6/bin 里的virtualenv和virtualenvwrapper)
pyenv global 3.6.6

# edy@edydeMacBook-Pro ~ % python -V
Python 3.6.6
# edy@edydeMacBook-Pro ~ % pip -V
pip 10.0.1 from /Users/edy/.pyenv/versions/3.6.6/lib/python3.6/site-packages/pip (python 3.6)
# edy@edydeMacBook-Pro ~ % pip3 -V
pip 10.0.1 from /Users/edy/.pyenv/versions/3.6.6/lib/python3.6/site-packages/pip (python 3.6)

# 安装:
sudo pip install virtualenvwrapper
# 或(现在pip和pip3是一样的)
sudo pip3 install virtualenvwrapper

# 成功
# edy@edydeMacBook-Pro bin % cd ~/.pyenv/versions/3.6.6/bin
# edy@edydeMacBook-Pro bin % ls -rtli | grep virtualenv
12891481885 -rwxr-xr-x  1 root  staff     2210  2 10  2019 virtualenvwrapper_lazy.sh
12891481886 -rwxr-xr-x  1 root  staff    41703  2 10  2019 virtualenvwrapper.sh
12891481528 -rwxr-xr-x  1 root  staff      272  2 14 17:27 virtualenv
12891481542 -rwxr-xr-x  1 root  staff      248  2 14 17:27 virtualenv-clone

# edy@edydeMacBook-Pro bin % cd /usr/local/bin
# edy@edydeMacBook-Pro bin % ls -rtli | grep virtualenv
12891478576 -rwxr-xr-x  1 root  admin     321  2 14 17:16 virtualenv
12891478950 -rwxr-xr-x  1 root  admin    2210  2 14 17:18 virtualenvwrapper_lazy.sh
12891478951 -rwxr-xr-x  1 root  admin   41703  2 14 17:18 virtualenvwrapper.sh
12891479428 -rwxr-xr-x  1 root  admin     510  2 14 17:18 virtualenv-clone

######### 配置virtualenvwrapper #########

# 创建一个文件夹(隐藏文件夹，不易被别人误删)，来存放虚拟环境
mkdir ~/.pyvirs

# 在使用virtualenvwrapper之前，要运行virtualenvwrapper.sh文件，需要设置环境变量，添加到~/.bash_profile 或 ~/.中
# 1
export WORKON_HOME=~/.pyvirs             # 指明，虚拟环境安装的目录
# 2
source /usr/local/bin/virtualenvwrapper.sh      # 使用，该virtualenvwrapper脚本
# 或
source $HOME/.pyenv/versions/3.6.6/bin/virtualenvwrapper.sh    # 安装的时候，其实/usr/local/bin/virtualenvwrapper.sh是这个文件的副本
# 设置环境变量
vi ~/.zshrc
# 或(有的mac用的是这个)
vi ~/.base_profile
'''
# virtualenv PATH
export WORKON_HOME=$HOME/.pyvirs
export VIRTUALENVWRAPPER_PYTHON=$HOME/.pyenv/versions/3.6.6/bin/python
export VIRTUALENVWRAPPER_VIRTUALENV=$HOME/.pyenv/versions/3.6.6/bin/virtualenv
source $HOME/.pyenv/versions/3.6.6/bin/virtualenvwrapper.sh
'''

# 然后，执行此命令加载环境即可，(.pyvirs如果不存在则自动创建)
# edy@edydeMacBook-Pro ~ % source .zshrc
virtualenvwrapper.user_scripts creating /Users/edy/.pyvirs/premkproject
virtualenvwrapper.user_scripts creating /Users/edy/.pyvirs/postmkproject
virtualenvwrapper.user_scripts creating /Users/edy/.pyvirs/initialize
virtualenvwrapper.user_scripts creating /Users/edy/.pyvirs/premkvirtualenv
virtualenvwrapper.user_scripts creating /Users/edy/.pyvirs/postmkvirtualenv
virtualenvwrapper.user_scripts creating /Users/edy/.pyvirs/prermvirtualenv
virtualenvwrapper.user_scripts creating /Users/edy/.pyvirs/postrmvirtualenv
virtualenvwrapper.user_scripts creating /Users/edy/.pyvirs/predeactivate
virtualenvwrapper.user_scripts creating /Users/edy/.pyvirs/postdeactivate
virtualenvwrapper.user_scripts creating /Users/edy/.pyvirs/preactivate
virtualenvwrapper.user_scripts creating /Users/edy/.pyvirs/postactivate
virtualenvwrapper.user_scripts creating /Users/edy/.pyvirs/get_env_details
# edy@edydeMacBook-Pro ~ % cd .pyvirs
# edy@edydeMacBook-Pro .pyvirs % ls
get_env_details		postactivate		postmkproject		postrmvirtualenv	predeactivate		premkvirtualenv
initialize		postdeactivate		postmkvirtualenv	preactivate		premkproject		prermvirtualenv

# 查看助手
virtualenv --help
```

### 总结

环境变量

```bash
# Python虚拟环境的如何配置呢？依据是什么？
# 答案:
# 其实目的就是为了合理使用 source /xx/xx/virtualenvwrapper.sh 脚本，所以查看下这个脚本就一目了然了。
# cat $HOME/.pyenv/versions/3.6.6/bin/virtualenvwrapper.sh

# 为啥还设置了 VIRTUALENVWRAPPER_PYTHON, VIRTUALENVWRAPPER_VIRTUALENV, VIRTUALENVWRAPPER_VIRTUALENV_CLONE ?
# 原因:
# 因为本电脑上安装了多个不同版本的Python, 随时可能会切换, 有的可能没有安装virtualenv, 如果不指定会默认去找系统的bin安装的python,virtualenv, virtualenv-clone, 所以直接指定下哪一个就好了。

# 注意:
# 1. 虽然我们一开始用python2.7的pip安装的virtualenv, 但是后来virtualenvwrapper安装不了, 所以用的是python3.6.6环境。
# 2. 也就是说，最终使用的 virtualenv, virtualenvwrapper 都是 python3.6.6 里的，跟python2.7没有任何关系了。

# python virtualenv
export WORKON_HOME=$HOME/.pyvirs
export VIRTUALENVWRAPPER_PYTHON=$HOME/.pyenv/versions/3.6.6/bin/python
export VIRTUALENVWRAPPER_VIRTUALENV=$HOME/.pyenv/versions/3.6.6/bin/virtualenv
export VIRTUALENVWRAPPER_VIRTUALENV_CLONE=$HOME/.pyenv/versions/3.6.6/bin/virtualenv-clone
export VIRTUALENVWRAPPER_SCRIPT=$HOME/.pyenv/versions/3.6.6/bin/virtualenvwrapper.sh
source $VIRTUALENVWRAPPER_SCRIPT
```

常用命令

```bash
######## 以下为工作使用的实际问题，即操作 #############

# 查看此~/.pyvirs 已有的虚拟环境
workon

# 创建3.7.0的虚拟环境（本质，就是在.pyvirs 目录下，多了一个py370_cmdb目录而已，每多一个就是多一个虚拟环境）

# 以当前的 python (pyenv可以切换)生成一个虚拟环境:py370_cmdb
mkvirtualenv py370_cmdb
# 以指定python3.6.6生成一个虚拟环境:py366_cmdb
mkvirtualenv -p ~/.pyenv/versions/3.6.6/bin/python py366_cmdb

# 怎么得到一个纯净的虚拟环境，如下（加一个选项）：
mkvirtualenv --no-site-packages py370_cmdb
如：
mkvirtualenv -p ~/.pyenv/versions/3.6.6/bin/python --no-site-packages py366_cmdb

# 如果有错误，这里说明原因:
mkvirtualenv --site-no-packages py370-web
# virtualenv: error: unrecognized arguments: --site-no-packages
# SystemExit: 2
# 原因:
virtualenv --version
# virtualenv 20.13.1 from /Users/edy/.pyenv/versions/3.6.6/lib/python3.6/site-packages/virtualenv/__init__.py
# 使用virtualenv --version，看到自己的版本大于20，从版本20开始，默认就是’–no-site-packages‘了
# 参数--no-site-packages，已经安装到系统 Python 环境中，Python第三方包不会复制过来

# 纯净环境一般就只有三个python包
# (py366) edy@edydeMacBook-Pro ~ % pip list
'''
Package    Version
---------- -------
pip        21.3.1
setuptools 59.6.0
wheel      0.37.1
'''

# 删除一个环境变量
rmvirtualenv py366_cmdb

# 另外，在虚拟环境中的一些命令：
pip list     # 包含Python自带的所有包
pip freeze    # 安装的额外的依赖包

pip install -r requirements.txt      # 导出
pip freeze > requirements.txt        # 导入并安装所有

pip install flask==0.10.1          # 安装指定版本

pip -V
python -V

deactivate       # 退出当前虚拟环境
```
