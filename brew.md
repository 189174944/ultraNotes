# 网上的[更新](https://javaforall.cn/tag/更新)国内源大多不完整，导致brew update 失败

# 先更新下brew

有时brew版本太旧也会有问题

```javascript
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

------

# 再更新国内源

```javascript
#更新Homebrew
cd "$(brew --repo)"
git remote set-url origin https://mirrors.ustc.edu.cn/brew.git

#更新Homebrew-core
cd "$(brew --repo)/Library/Taps/homebrew/homebrew-core"
git remote set-url origin https://mirrors.ustc.edu.cn/homebrew-core.git

#更新Homebrew-cask（最重要的一步，很多更新完国内源依然卡就是没更新这个）
cd "$(brew --repo)"/Library/Taps/homebrew/homebrew-cask
git remote set-url origin https://mirrors.ustc.edu.cn/homebrew-cask.git
```

------

# 更新HOMEBREW_BOTTLE_DOMAIN

最重要

- 使用zsh的用户

```javascript
echo 'export HOMEBREW_BOTTLE_DOMAIN=https://mirrors.ustc.edu.cn/homebrew-bottles/' >> ~/.zshrc
source ~/.zshrc
```

- 使用bash的用户

```javascript
echo 'export HOMEBREW_BOTTLE_DOMAIN=https://mirrors.ustc.edu.cn/homebrew-bottles/' >> ~/.bash_profile
source ~/.bash_profile
```

------

# 更新库

```javascript
brew update -v
#或都使用下面的更新
```

~~brew update-reset && brew update -v -f~~

***感谢网友提醒，使用下面的命令即可***

```javascript
brew update-reset 
```