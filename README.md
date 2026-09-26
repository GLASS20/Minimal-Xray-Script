# Xray 安装脚本

本仓库提供了一键安装和配置 Xray-core 的 shell 脚本。该脚本自动完成下载最新的 Xray 版本，设置为 OpenRC 服务，并配置一个基础的 SOCKS 代理。

## 安装方法
使用以下命令安装：

Alpine
```sh
wget https://raw.githubusercontent.com/GLASS20/Minimal-Xray-Script/refs/heads/main/alpine-install.sh && bash alpine-install.sh
```

Debian
```sh
wget https://raw.githubusercontent.com/GLASS20/Minimal-Xray-Script/refs/heads/main/debian-install.sh && bash debian-install.sh
```

## 管理 Xray 服务
安装完成后，可以使用 OpenRC 命令来管理 Xray 服务：

### 启动 Xray 服务：
```sh
sudo service xray start
```

### 停止 Xray 服务：
```sh
sudo service xray stop
```

### 重启 Xray 服务：
```sh
sudo service xray restart
```

代码来自https://github.com/miku111/XrayOnAlpine

### 查看 Xray 服务状态：
```sh
sudo service xray status
```
