> origin doc address: https://juejin.cn/post/7083026831263137800
---
#### 第一步:删除现有Node版本
```shell
brew uninstall --ignore-dependencies node
brew uninstall --force node
```
#### 第二步:在Mac上安装NVM
```shell
brew update
brew install nvm
```
在home目录中为NVM创建一个文件夹并配置所需的环境变量
```shell
mkdir ~/.nvm
vim ~/.bash_profile  ## 或者vim ~/.zshrc
export NVM_DIR=~/.nvm
source $(brew --prefix nvm)/nvm.sh
source ~/.bash_profile ## 或者source ~/.zshrc
```
#### 第三步 : 用NVM安装Node.js
```shell
nvm ls-remote
nvm install node ## 安装最后一个长期支持版本
nvm ls
nvm use version ## 选择需要安装的版本
```