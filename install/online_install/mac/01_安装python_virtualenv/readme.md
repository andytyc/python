<!--ts-->

- [总结干货](#总结干货)
  - [python 安装](#python-安装)
  - [python 虚拟环境](#python-虚拟环境)
- [实战笔记](#实战笔记)

<!-- Added by: edy, at: 2023年 3月13日 星期一 11时02分31秒 CST -->

<!--te-->

# 总结干货

> 直接将安装过程总结，直接说重点

## python 安装

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

## python 虚拟环境

环境变量

```bash
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

# 进入虚拟环境 py366_cmdb
workon py366_cmdb

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

# 实战笔记

> 记录下安装的过程备注下，平时参考 `总结笔记` 就可以了

- [环境配置 env](./env.md)
- [安装笔记](./install.md)
