# 问题集合



## Ubuntu 安装 git

```shell
sudo apt install -y git
```



## CentOS 安装 git

```shell
yum install -y git
```



## Git 配置

```shell
# 根据个人信息配置
git config --global user.name "Eniso92"
git config --global user.email "eniso-92@qq.com"

# 下面配置可选
git config --global core.quotepath false
git config --global gui.encoding utf-8
git config --global i18n.commit.encoding utf-8
git config --global i18n.logoutputencoding utf-8
```



## Windows 下汉字显示问题

```shell
git config --global core.quotepath false
git config --global gui.encoding utf-8
git config --global i18n.commit.encoding utf-8
git config --global i18n.logoutputencoding utf-8
# 临时显示中文，可以使用下面的命令，建议在环境变量中配置
set LESSCHARSET=utf-8
```

