# 红米AC2100 Openwrt trojan预编译包

## 说明

基于openwrt 21.02以及https://github.com/trojan-gfw/openwrt-trojan的文件编译而成

## 适用范围

红米AC2100刷新成带有pxxswall功能的21.02 openwrt固件后（如lienol版本），默认的trojan-go较为吃内存（go的gc机制所限，14M左右），容易oom，导致断网；另外还有一个原因是本人在rm2100上
安装了tailscale以使得以udp方式进行dns防污染操作（为了避免经由tcp查询导致的响应慢的问题），而tailscale同样是go编写，亦是内存占用大户（14M左右）。

改用trojan版本，内存占用为4M左右。

## 使用方式

1. 上传包到路由器/tmp目录
2. opkg install /tmp/boost*.ipk
3. opkg install /tmp/trojan*.ipk
4. mv /usr/bin/xray /usr/bin/xray.bak // 此步骤采用hack方式，使得passwall无法拉起xray，但仍能配置iptables、拉起dns等能力
5. 配置/etc/config/trojan，打开trojan
6. 配置/etc/trojan.json，配置线路

## 其他说明
1. trojan不支持tproxy能力，tcp代理需采用redirect模式
2. 默认的trojan.json是server模式，参考官网修改成nat模式即可
