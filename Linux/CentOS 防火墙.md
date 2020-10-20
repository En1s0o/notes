# CentOS 防火墙

## 基本使用

- 启动

  ```shell
  systemctl start firewalld
  ```

- 停止

  ```shell
  systemctl stop firewalld
  ```

- 查看状态

  ```shell
  systemctl status firewalld
  ```

- 禁用，禁止开机启动

  ```shell
  systemctl disable firewalld
  ```

 

## 配置 firewalld-cmd

- 查看版本

  ```shell
  firewall-cmd --version
  ```

- 查看帮助

  ```shell
  firewall-cmd --help
  ```

- 显示状态

  ```shell
  firewall-cmd --state
  ```

- 查看所有打开的端口

  ```shell
  firewall-cmd --zone=public --list-ports
  ```

- 更新防火墙规则

  ```shell
  firewall-cmd --reload
  ```

- 更新防火墙规则，重启服务

  ```shell
  firewall-cmd --completely-reload
  ```

- 查看已激活的 Zone 信息

  ```shell
  firewall-cmd --get-active-zones
  ```

- 查看指定接口所属区域

  ```shell
  firewall-cmd --get-zone-of-interface=eth0
  ```

- 拒绝所有包

  ```shell
  firewall-cmd --panic-on
  ```

- 取消拒绝状态

  ```shell
  firewall-cmd --panic-off
  ```

- 查看是否拒绝

  ```shell
  firewall-cmd --query-panic
  ```



## 信任级别

> 通过 --zone 参数指定

- `drop` 丢弃所有进入的包，而不给出任何响应 
- `block` 拒绝所有外部发起的连接，允许内部发起的连接 
- `public` 允许指定的进入连接 
- `external` 同上，对伪装的进入连接，一般用于路由转发 
- `dmz` 允许受限制的进入连接 
- `work` 允许受信任的计算机被限制的进入连接，类似 workgroup 
- `home` 同上，类似 homegroup 
- `internal` 同上，范围针对所有互联网用户 
- `trusted` 信任所有连接



## 开启/关闭端口

> 以下在 public 的 zone 下的操作

- 添加

  ```shell
  # --permanent 参数为“永久生效”
  firewall-cmd --zone=public --add-port=80/tcp --permanent
  ```

- 重新载入

  ```shell
  firewall-cmd --reload
  ```

- 查看

  ```shell
  firewall-cmd --zone=public --query-port=80/tcp
  ```

- 删除
  
  ```shell
  firewall-cmd --zone=public --remove-port=80/tcp --permanent
  ```



## 管理服务

> 以 smtp 服务为例，添加到 work zone

- 添加

  ```shell
  firewall-cmd --zone=work --add-service=smtp
  ```

- 查看

  ```shell
  firewall-cmd --zone=work --query-service=smtp
  ```

- 删除

  ```shell
  firewall-cmd --zone=work --remove-service=smtp
  ```



## 配置 IP 地址伪装

- 查看

  ```shell
  firewall-cmd --zone=external --query-masquerade
  ```

- 打开

  ```shell
  firewall-cmd --zone=external --add-masquerade
  ```

- 关闭

  ```shell
  firewall-cmd --zone=external --remove-masquerade
  ```



## 端口转发

- 打开端口转发，首先需要打开 IP 地址伪装

  ```shell
  firewall-cmd --zone=external --add-masquerade
  ```

- 转发 tcp 22 端口至 2222

  ```shell
  firewall-cmd --zone=external --add-forward-port=22:porto=tcp:toport=2222
  ```

- 转发端口数据至另一个 IP 的相同端口

  ```shell
  firewall-cmd --zone=external --add-forward-port=22:porto=tcp:toaddr=192.168.1.101
  ```

- 转发端口数据至另一个 IP 的 2222 端口

  ```shell
  firewall-cmd --zone=external --add-forward-port=22:porto=tcp:toport=2222:toaddr=192.168.1.101
  ```


