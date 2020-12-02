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



## SVN 迁移至 Git

- 账号对应

  ```shell
  svn log <repository> -q | awk -F '|' '/^r/ {sub("^ ", "", $2); sub(" $", "", $2); print $2"="$2" <"$2"@gmail.com>"}' | sort -u > ./svn2git.txt
  ```

  > 根据实际情况修改 `@gmail.com`。当生成的 svn2git.txt 不符合需求时，手动修改即可。

- 拉取代码

  ```shell
  git svn clone <repository> --no-metadata --authors-file="./svn2git.txt" <directory>
  ```

  > 如果没有附带 `--authors-file` 参数，生成的 git commit 信息中，邮箱域名是一个 uuid。

- 推送到 git 远程仓库

  ```shell
  git remote add origin <url>
  git push -u origin master
  ```



