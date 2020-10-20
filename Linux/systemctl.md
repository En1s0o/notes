# systemctl

> 适合 Ubuntu、CentOS 等 Linux 系统
>
> CentOS7 的服务管理工具中主要的工具，它融合之前 service 和 chkconfig 的功能于一体

- 启动一个服务

  ```shell
  systemctl start firewalld.service
  ```

- 关闭一个服务

  ```shell
  systemctl stop firewalld.service
  ```

- 重启一个服务

  ```shell
  systemctl restart firewalld.service
  ```

- 显示一个服务的状态

  ```shell
  systemctl status firewalld.service
  ```

- 在开机时启用一个服务

  ```shell
  systemctl enable firewalld.service
  ```

- 在开机时禁用一个服务

  ```shell
  systemctl disable firewalld.service
  ```

- 查看服务是否开机启动

  ```shell
  systemctl is-enabled firewalld.service
  ```

- 查看已启动的服务列表

  ```shell
  systemctl list-unit-files|grep enabled
  ```

- 查看启动失败的服务列表

  ```shell
  systemctl --failed
  ```

