# Samba 安装


## Ubuntu

- 安装

  ```shell
  sudo apt install -y samba
  ```

- 创建 samba 账户

  ```shell
  sudo smbpasswd -a eniso
  ```

  > 根据提示输入 samba 用户（这里是 `eniso`）的密码

- 配置

  vim /etc/samba/smb.conf

  假设：samba 用户为 eniso，允许访问 /home/eniso 路径

  ```
  [eniso]
     comment = Eniso Home Directories
     valid users = eniso
     path = /home/eniso
     public = yes
     browseable = yes
     writable = yes
     follow symlinks = yes
     wide links = yes
     unix extensions = no
  ```

- 启动 samba 服务

  ```shell
  sudo systemctl stop smbd.service
  sudo systemctl start smbd.service
  # 开机自启动
  sudo systemctl enable smbd.service
  ```



## CentOS

- 安装

  ```shell
  yum install -y samba
  ```

- 创建 samba 账户

  ```shell
  sudo smbpasswd -a root
  ```

  > 根据提示输入 samba 用户（这里是 `root`）的密码

- 配置

  vim /etc/samba/smb.conf

  假设：samba 用户为 root，允许访问 /root 路径

  ```
  [root]
      comment = Root Home Directories
      valid users = root
      path = /root
      public = yes
      browseable = yes
      writable = yes
      follow symlinks = yes
      wide links = yes
      unix extensions = no
  ```

- 关闭 SELinux

  ```shell
  # 临时关闭
  setenforce 0
  # 永久关闭
  sed -i 's/SELINUX=enforcing/SELINUX=disabled/g' /etc/sysconfig/selinux
  # 可以通过 getenforce 查看状态
  ```

- 开放端口

  ```shell
  # --permanent 参数为“永久生效”
  firewall-cmd --zone=public --add-port=139/tcp --permanent
  firewall-cmd --zone=public --add-port=445/tcp --permanent
  firewall-cmd --zone=public --add-port=137/udp --permanent
  firewall-cmd --zone=public --add-port=138/udp --permanent
  # 更新防火墙规则
  firewall-cmd --reload
  ```

- 启动 samba 服务

  ```shell
  systemctl stop smb.service
  systemctl start smb.service
  # 开机自启动
  systemctl enable smb.service
  ```

