# 操作与排错：检测、日志、规则、IPv6

## 示例 Clash 规则为什么合理

示例规则是“本地直连 + 其他全代理”：

```text
DOMAIN-SUFFIX,local,DIRECT
IP-CIDR,10.0.0.0/8,DIRECT,no-resolve
IP-CIDR,172.16.0.0/12,DIRECT,no-resolve
IP-CIDR,192.168.0.0/16,DIRECT,no-resolve
IP-CIDR,127.0.0.0/8,DIRECT,no-resolve
MATCH,PROXY
```

含义：

```text
.local:
本地域名直连

10/8、172.16/12、192.168/16:
内网地址直连

127/8:
本机回环直连

MATCH:
其他公网流量走代理
```

效果：

```text
局域网 / 本机开发 / 路由器管理页 -> 不走代理
公网网站 / App 外网请求 -> 入口 VPS -> 静态 ISP 代理
```

这适合这个示例目标：外网流量走静态 ISP 出口，同时不破坏本机开发和局域网访问。

## 示例 DNS/IPv6 策略

示例 Clash profile 可以加入：

```yaml
dns:
  enable: true
  ipv6: false
  enhanced-mode: fake-ip
  respect-rules: true
  nameserver:
    - https://1.1.1.1/dns-query
    - https://1.0.0.1/dns-query
```

示例检测方向：

```text
IPv4 = 198.51.100.20
DNS = 美国 Cloudflare / 代理侧
IPv6 = not reachable / 不显示真实公网 IPv6
```

## 常用检测网站

```text
api.ipify.org
ipinfo.io
ipleak.net
browserleaks.com/ip
browserleaks.com/dns
test-ipv6.com
Scamalytics
AbuseIPDB
```

看：

```text
出口 IP
DNS 地区和组织
IPv6 是否泄漏
WebRTC 是否暴露
IP 纯净度
滥用记录
```

## 常见排错分层

VPS 服务是否活着：

```bash
systemctl is-active xray
```

Xray 配置是否正确：

```bash
/usr/local/bin/xray run -test -config /usr/local/etc/xray/config.json
```

VPS 是否监听 443：

```bash
ss -lntp | grep ':443 '
```

VPS 到静态 ISP 代理是否通：

```bash
curl --socks5 代理地址:端口 -U '用户名:密码' --max-time 15 https://api.ipify.org
```

客户端重点看：

```text
server IP
port
uuid
public-key
short-id
sni
flow
```

本机重点看：

```text
是否有另一个 TUN/VPN 客户端开着
Clash Verge TUN 是否开着
是否同时开了多个 VPN/代理 App
规则是否 DIRECT
DNS 是否代理侧
IPv6 是否泄漏
```

## 网页控制台和 systemctl

`Command transmission error` 这类报错通常是 VPS 网页控制台没有把命令发出去，不等于 Linux 命令失败。

处理：

```text
一行一行粘贴命令
刷新网页 shell
必要时在服务商控制台重启 VPS
```

`systemctl restart xray` 的作用：

```text
停止旧 Xray
用新 config.json 启动 Xray
```

如果 restart 卡在网页控制台，但配置已写入磁盘，可以重启 VPS。
