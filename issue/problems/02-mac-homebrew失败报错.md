<!--ts-->
   * [问题.brew install python3 失败](#问题brew-install-python3-失败)
      * [问题](#问题)
      * [解决](#解决)

<!-- Added by: edy, at: 2022年 2月14日 星期一 15时05分04秒 CST -->

<!--te-->

# 问题.brew install python3 失败

## 问题

```bash
# 之前的错误信息忘记备注了，以后遇到可以再加上
```

## 解决

```bash
# 自己的笔记:
# https://blog.csdn.net/weixin_41957017/article/details/84644635
```

使用的是 ustc 国内镜像源, 自己手动查看是否配置源正确，是否最新 pull 的源代码。

```bash
############## 之前安装homebrew后，替换国内镜像的操作 ##############

# 更换为中科院的镜像
git clone git://mirrors.ustc.edu.cn/homebrew-core.git/ /usr/local/Homebrew/Library/Taps/homebrew/homebrew-core --depth=1

cd "$(brew --repo)"
git remote set-url origin https://mirrors.ustc.edu.cn/brew.git
cd "$(brew --repo)/Library/Taps/homebrew/homebrew-core"
git remote set-url origin https://mirrors.ustc.edu.cn/homebrew-core.git
cd "$(brew --repo)/Library/Taps/homebrew/homebrew-cask"
git remote set-url origin https://mirrors.ustc.edu.cn/homebrew-cask.git

bash（默认 shell）用户：
echo 'export HOMEBREW_BOTTLE_DOMAIN=https://mirrors.ustc.edu.cn/homebrew-bottles' >> ~/.bash_profile
source ~/.bash_profile

zsh 用户：
echo 'export HOMEBREW_BOTTLE_DOMAIN=https://mirrors.ustc.edu.cn/homebrew-bottles' >> ~/.zshrc

############## 这次报错，来手动更新下代码看看 ##############
cd "$(brew --repo)"
git branch
# master
git pull

cd "$(brew --repo)/Library/Taps/homebrew/homebrew-core"
git branch
# master
git pull

cd "$(brew --repo)/Library/Taps/homebrew/homebrew-cask"
git branch
# master
git pull

# 然后，再次brew install python3 就可以了，这个可能是这个原因，也可能是之前python2,python3有问题，通过检查自带的python2和之前就有安装的python3，梳理好后解决的，不管了，这里备注下。
```
