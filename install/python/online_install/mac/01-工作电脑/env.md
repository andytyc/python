执行 `vi ~/.zshrc`

```bash
# homebrew-bottles env
export HOMEBREW_BOTTLE_DOMAIN=https://mirrors.ustc.edu.cn/homebrew-bottles

##################### python #####################

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

# python virtualenv path
export WORKON_HOME=$HOME/.pyvirs
export VIRTUALENVWRAPPER_PYTHON=$HOME/.pyenv/versions/3.6.6/bin/python
export VIRTUALENVWRAPPER_VIRTUALENV=$HOME/.pyenv/versions/3.6.6/bin/virtualenv
export VIRTUALENVWRAPPER_VIRTUALENV_CLONE=$HOME/.pyenv/versions/3.6.6/bin/virtualenv-clone
export VIRTUALENVWRAPPER_SCRIPT=$HOME/.pyenv/versions/3.6.6/bin/virtualenvwrapper.sh
source $VIRTUALENVWRAPPER_SCRIPT

##################### python #####################

```
