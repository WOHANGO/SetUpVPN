
# IPSec VPN 服务器

[![GitHub Stars](https://img.shields.io/github/stars/WOHANGO/SetUpVPN.svg?maxAge=86400)](https://github.com/WOHANGO/SetUpVPN/stargazers)

# 简介
这个是基于Linux环境下搭建IPSec VPN服务器，有什么问题可以<a href="https://github.com/WOHANGO/SetUpVPN/issues/new" target="_blank">留言</a>，顺便求<a href="https://github.com/WOHANGO/SetUpVPN/stargazers" target="_blank">⭐️⭐️⭐️⭐️⭐️⭐️⭐️⭐️⭐️</a>~（网页右上角：🌟Star）

使用 Linux 搭建自己的 IPsec VPN 服务器。支持 IPsec/L2TP 和 Cisco IPsec 协议，可用于 Ubuntu/Debian/CentOS 系统。你只需提供自己的 VPN 登录凭证即可自动完成安装。

IPsec VPN 可以加密你的网络流量，以防止在通过互联网传送数据时，你和 VPN 服务器之间的任何人对你的数据的未经授权的访问。

<a href="https://blog.ls20.com/ipsec-l2tp-vpn-auto-setup-for-ubuntu-12-04-on-amazon-ec2/" target="_blank">**&raquo; 相关教程： IPsec VPN Server Auto Setup with Libreswan**</a>

#### 目录

- [快速开始](#快速开始)
- [功能特性](#功能特性)
- [系统要求](#系统要求)
- [安装说明](#安装说明)
- [下一步](#下一步)

## 快速开始

首先，我们需要一台国外的服务器，系统可以为Linux、Ubuntu、CentOS……（只要是Linux系统就行）。

本人使用的服务器是在<a href="https://bwh1.net/clientarea.php?action=products" target="_blank">BandwagonHOST</a>购买的，价钱为$2.99/月

使用以下命令快速搭建 IPsec VPN 服务器：

```bash
wget https://git.io/vpnsetup -O vpnsetup.sh && sudo sh vpnsetup.sh
```

如果使用 CentOS，请将上面的地址换成 `https://git.io/vpnsetup-centos`。

你的 VPN 登录凭证将会被自动随机生成，并在安装完成后显示在屏幕上。

如需了解其它安装选项，以及如何配置 VPN 客户端，请继续阅读以下部分。

<a name="quick-start-note"></a>
\* 一个专用服务器或者虚拟专用服务器 (VPS)。OpenVZ VPS 不受支持。

## 功能特性

- **新:** 增加支持更高效的 `IPsec/XAuth ("Cisco IPsec")` 模式
- **新:** 现在可以下载 VPN 服务器的预构建 <a href="https://github.com/hwdsl2/docker-ipsec-vpn-server/blob/master/README-zh.md" target="_blank">Docker 镜像</a>
- 全自动的 IPsec VPN 服务器配置，无需用户输入
- 封装所有的 VPN 流量在 UDP 协议，不需要 ESP 协议支持
- 可直接作为 Amazon EC2 实例创建时的用户数据使用
- 包含 `sysctl.conf` 优化设置，以达到更佳的传输性能
- 已测试： Ubuntu 16.04/14.04， Debian 9/8 和 CentOS 7/6

## 系统要求

一个新创建的 <a href="https://aws.amazon.com/ec2/" target="_blank">Amazon EC2</a> 实例，使用这些映像 (AMIs):
- <a href="https://cloud-images.ubuntu.com/locator/" target="_blank">Ubuntu 16.04 (Xenial) or 14.04 (Trusty)</a>
- <a href="https://wiki.debian.org/Cloud/AmazonEC2Image" target="_blank">Debian 9 (Stretch) or 8 (Jessie)</a>
- <a href="https://aws.amazon.com/marketplace/pp/B00O7WM7QW" target="_blank">CentOS 7 (x86_64) with Updates</a>
- <a href="https://aws.amazon.com/marketplace/pp/B00NQAYLWO" target="_blank">CentOS 6 (x86_64) with Updates</a>

请参见 <a href="https://blog.ls20.com/ipsec-l2tp-vpn-auto-setup-for-ubuntu-12-04-on-amazon-ec2/#vpnsetup" target="_blank">详细步骤</a> 以及 <a href="https://aws.amazon.com/cn/ec2/pricing/" target="_blank">EC2 定价细节</a>。

**-或者-**

一个专用服务器，或者基于 KVM/Xen 的虚拟专用服务器 (VPS)，全新安装以上操作系统之一。OpenVZ VPS 不受支持，用户可以另外尝试比如 <a href="https://shadowsocks.org" target="_blank">Shadowsocks</a> 或者 <a href="https://github.com/Nyr/openvpn-install" target="_blank">OpenVPN</a>。

这也包括各种公共云服务中的 Linux 虚拟机，比如 <a href="https://blog.ls20.com/digitalocean" target="_blank">DigitalOcean</a>, <a href="https://blog.ls20.com/vultr" target="_blank">Vultr</a>, <a href="https://blog.ls20.com/linode" target="_blank">Linode</a>, <a href="https://cloud.google.com/compute/" target="_blank">Google Compute Engine</a>, <a href="https://amazonlightsail.com" target="_blank">Amazon Lightsail</a>, <a href="https://azure.microsoft.com" target="_blank">Microsoft Azure</a>, <a href="https://www.ibm.com/cloud-computing/bluemix/virtual-servers" target="_blank">IBM Bluemix</a>, <a href="https://www.ovh.com/us/vps/" target="_blank">OVH</a> 和 <a href="https://www.rackspace.com" target="_blank">Rackspace</a>。

<a href="azure/README-zh.md" target="_blank"><img src="docs/images/azure-deploy-button.png" alt="Deploy to Azure" /></a> <a href="http://dovpn.carlfriess.com/" target="_blank"><img src="docs/images/do-install-button.png" alt="Install on DigitalOcean" /></a> <a href="https://www.linode.com/stackscripts/view/37239" target="_blank"><img src="docs/images/linode-deploy-button.png" alt="Deploy to Linode" /></a>

<a href="https://blog.ls20.com/ipsec-l2tp-vpn-auto-setup-for-ubuntu-12-04-on-amazon-ec2/#gettingavps" target="_blank">**&raquo; 我想建立并使用自己的 VPN ，但是没有可用的服务器**</a>

高级用户可以在 $35 <a href="https://blog.elasticbyte.net/setting-up-a-native-cisco-ipsec-vpn-server-using-a-raspberry-pi/" target="_blank">Raspberry Pi 3</a> 上搭建 VPN 服务器。

:warning: **不要** 在你的 PC 或者 Mac 上运行这些脚本！它们只能用在服务器上！

## 安装说明

### Ubuntu & Debian

首先，更新你的系统： 运行 `apt-get update && apt-get dist-upgrade` 并重启。这一步是可选的，但推荐。

要安装 VPN，请从以下选项中选择一个：

**选项 1:** 使用脚本随机生成的 VPN 登录凭证 （完成后会在屏幕上显示）：

```bash
wget https://git.io/vpnsetup -O vpnsetup.sh && sudo sh vpnsetup.sh
```

**选项 2:** 编辑脚本并提供你自己的 VPN 登录凭证：

```bash
wget https://git.io/vpnsetup -O vpnsetup.sh
nano -w vpnsetup.sh
[替换为你自己的值： YOUR_IPSEC_PSK, YOUR_USERNAME 和 YOUR_PASSWORD]
sudo sh vpnsetup.sh
```

**选项 3:** 将你自己的 VPN 登录凭证定义为环境变量：

```bash
# 所有变量值必须用 '单引号' 括起来
# *不要* 在值中使用这些字符：  \ " '
wget https://git.io/vpnsetup -O vpnsetup.sh && sudo \
VPN_IPSEC_PSK='你的IPsec预共享密钥' \
VPN_USER='你的VPN用户名' \
VPN_PASSWORD='你的VPN密码' sh vpnsetup.sh
```

**注：** 如果无法通过 `wget` 下载，你也可以打开 <a href="vpnsetup.sh" target="_blank">vpnsetup.sh</a> (或者 <a href="vpnsetup_centos.sh" target="_blank">vpnsetup_centos.sh</a>)，然后点击右方的 **`Raw`** 按钮。按快捷键 `Ctrl-A` 全选， `Ctrl-C` 复制，然后粘贴到你喜欢的编辑器。

### CentOS & RHEL

首先，更新你的系统： 运行 `yum update` 并重启。这一步是可选的，但推荐。

按照与上面相同的步骤，但是将 `https://git.io/vpnsetup` 换成 `https://git.io/vpnsetup-centos`。

## 下一步

配置你的计算机或其它设备使用 VPN 。请参见：

<a href="docs/clients-zh.md" target="_blank">**配置 IPsec/L2TP VPN 客户端**</a>

<a href="docs/clients-xauth-zh.md" target="_blank">**配置 IPsec/XAuth ("Cisco IPsec") VPN 客户端**</a>

<a href="docs/ikev2-howto-zh.md" target="_blank">**如何配置 IKEv2 VPN: Windows 和 Android**</a>

如果在连接过程中遇到错误，请参见 <a href="docs/clients-zh.md#故障排除" target="_blank">故障排除</a>。

开始使用自己的专属 VPN ! :sparkles::tada::rocket::sparkles:


