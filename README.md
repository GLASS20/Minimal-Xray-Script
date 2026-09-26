# Xray 安装脚本

本仓库提供一键安装和配置 **Xray-core** 的 Shell 脚本，适用于 **Alpine Linux** 和 **Debian 13 x86_64**。

脚本可以自动下载最新版本的 Xray-core，并配置 **VLESS + REALITY**。同时保留 Hysteria 2 的安装选项。

## 功能

* 自动检测并下载最新版本 Xray-core
* 支持 **Debian 13 x86_64**
* 支持 Xray **VLESS + REALITY**
* 支持自动配置 REALITY
* 支持按地区选择 REALITY Target / SNI
* 自动生成 UUID、REALITY Private Key / Public Key 和 Short ID
* 自动生成客户端 VLESS URI
* Xray 配置文件自动进行语法检查
* 自动设置 Xray 开机启动
* 支持安装 Hysteria 2
* 下载的 Xray 压缩包支持 SHA-256 校验

## 安装方法

### Alpine Linux

```sh
wget https://raw.githubusercontent.com/GLASS20/Minimal-Xray-Script/refs/heads/main/alpine-install.sh
bash alpine-install.sh
```

### Debian 13 x86_64

```sh
wget https://raw.githubusercontent.com/GLASS20/Minimal-Xray-Script/refs/heads/main/debian-install.sh
bash debian-install.sh
```

> Debian 版本针对 **Debian 13 (trixie) x86_64** 进行适配。

## Xray 配置

运行安装脚本后，可以选择：

```text
1) install Xray and Config Reality
2) install Hysteria 2
```

选择 Xray 后，可以进一步选择：

```text
1) Auto Config (Amazon target)
2) Manual/Regional Config
3) Exit
```

### 自动配置

自动配置使用：

```text
Target: www.amazon.com:443
SNI:    www.amazon.com
```

脚本会自动生成：

* UUID
* REALITY Private Key
* REALITY Public Key
* Short ID

并生成 VLESS REALITY 客户端连接 URI。

配置完成后，客户端参数会保存到：

```text
/root/xray-reality.txt
```

### 区域配置

区域配置提供以下选项：

```text
1. US
2. UK
3. JP
4. HK
5. TW
6. SG
7. FR
8. DE
9. IN
10. Others
```

选择对应区域后，脚本会自动生成对应的 REALITY Target 和 SNI。

## 管理 Xray 服务

### Debian 13

Debian 版本使用 **systemd** 管理 Xray 服务。

启动：

```sh
sudo systemctl start xray
```

停止：

```sh
sudo systemctl stop xray
```

重启：

```sh
sudo systemctl restart xray
```

查看状态：

```sh
sudo systemctl status xray
```

设置开机启动：

```sh
sudo systemctl enable xray
```

取消开机启动：

```sh
sudo systemctl disable xray
```

查看日志：

```sh
sudo journalctl -u xray -n 100 --no-pager
```

实时查看日志：

```sh
sudo journalctl -u xray -f
```

## Xray 配置文件

Xray 主程序：

```text
/usr/local/bin/xray/xray
```

命令行软链接：

```text
/usr/local/sbin/xray
```

配置文件：

```text
/usr/local/etc/xray/config.json
```

Xray 数据文件：

```text
/usr/local/share/xray/
```

日志目录：

```text
/var/log/xray/
```

systemd 服务文件：

```text
/etc/systemd/system/xray.service
```

## 检查 Xray 配置

可以使用以下命令检查配置文件：

```sh
sudo /usr/local/bin/xray/xray run -test \
  -format json \
  -c /usr/local/etc/xray/config.json
```

如果配置正确，Xray 会通过配置检查。

也可以直接使用：

```sh
sudo systemctl restart xray
```

如果启动失败，可以查看：

```sh
sudo journalctl -u xray -n 100 --no-pager
```

## Hysteria 2

脚本同时提供 Hysteria 2 安装选项。

选择：

```text
2) install Hysteria 2
```

安装完成后，配置文件位于：

```text
/etc/hysteria/config.yaml
```

程序：

```text
/usr/local/bin/hysteria
```

服务文件：

```text
/etc/systemd/system/hysteria.service
```

管理 Hysteria 2：

```sh
sudo systemctl start hysteria
sudo systemctl stop hysteria
sudo systemctl restart hysteria
sudo systemctl status hysteria
```

查看日志：

```sh
sudo journalctl -u hysteria -n 100 --no-pager
```

## 源代码

本项目部分代码参考：
https://github.com/miku111/XrayOnAlpine
