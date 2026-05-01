# DNS：解析、调度、泄漏和缓存

## DNS 是电话黄页

域名是给人看的名字，IP 是机器真正连接的地址。

```text
人类输入:
www.example.com

DNS 查询后得到:
203.0.113.34

浏览器实际连接:
203.0.113.34
```

心智模型：

```text
域名 = 人类好记的名字
DNS = 查名字对应号码的电话黄页
IP = 机器真正拨过去的号码
服务器 = 接电话的人
HTTPS = 这通电话是加密的
代理/VPS = 替你打这通电话的人
```

## 为什么 DNS 也是一串数字

DNS 不是一串数字，DNS 服务器自己也有 IP 地址。

```text
1.1.1.1 = Cloudflare 递归 DNS
8.8.8.8 = Google 递归 DNS
114.114.114.114 = 常见中国公共 DNS
```

区分：

```text
DNS 服务器地址 = 查询谁
域名解析结果 = DNS 返回目标网站在哪
```

检测页显示的 DNS Addresses，指的是“帮用户查域名的 DNS 服务器出口”，不是代理出口 IP。

## DNS 是怎么解析 IP 的

```text
用户设备
-> 递归 DNS
-> 根 DNS
-> 顶级域 DNS
-> 权威 DNS
-> 返回目标 IP
```

常见记录：

```text
A     IPv4
AAAA  IPv6
CNAME 域名别名
MX    邮件服务器
TXT   文本记录
```

## 本地 DNS 设置应该填哪一层

Mac、iPhone、路由器里手动设置的 DNS，应该填递归 DNS。

适合填：

```text
1.1.1.1
8.8.8.8
9.9.9.9
运营商自动 DNS
路由器地址，例如 192.168.1.1
```

不适合填：

```text
根 DNS
.com 顶级域 DNS
google.com 的权威 DNS
```

本地 DNS 的意思是：“以后我查域名，就让这个服务器帮我一路查到底。”

比喻：

```text
本地配置的 DNS = 辖区片警 / 派出所窗口
根 DNS = 总目录
顶级域 DNS = 上级分类目录
权威 DNS = 具体责任单位
```

## 为什么 DNS 不做一张全球大表

直觉上可以做：

```text
域名 -> IP
```

但现实不可行：

```text
数据量巨大
更新频繁
权责分散
单点风险太高
大型网站需要动态调度
```

DNS 的核心架构是：

```text
分层授权 + 递归查询 + 本地缓存
```

递归 DNS 的缓存就是局部临时 LUT。第一次可能完整查询，TTL 过期前可以直接从缓存返回。

## DNS 会看人下菜碟

大型网站会根据查询来源返回不同 IP：

```text
GeoDNS
DNS-based load balancing
CDN 调度
Anycast
```

影响因素：

```text
DNS 查询来源
递归 DNS 所在地区
EDNS Client Subnet
节点负载
运营商线路质量
服务商调度策略
```

Google、Microsoft、Apple、Netflix、Cloudflare、Akamai 都会在全球部署大量节点，同一个域名从不同地区查，可能返回不同 IP。

## DNS 泄漏

理想状态：

```text
网页连接出口 = 代理出口地区
DNS 查询出口 = 代理出口地区
```

坏状态：

```text
网页连接 = 美国代理
DNS 查询 = 本地运营商
```

风险：

```text
暴露真实网络环境
调度不一致
平台画像不一致
```

代理侧正常状态示例：

```text
出口 IP = 198.51.100.20
DNS = 美国 Cloudflare / 代理侧 DNS
```

## 系统 Wi-Fi DNS 和 Clash DNS

macOS Wi-Fi DNS 可能显示 `8.8.8.8` 或其他值，但 Clash/TUN 可以在更前面接管 DNS。

分层：

```text
Wi-Fi DNS = 系统网络服务默认 DNS
Clash DNS = mihomo 接管后实际使用的 DNS
检测页 DNS = 浏览器实际查询被处理后的结果
```

Clash 不一定改写 Wi-Fi DNS，而是拦截并处理查询。

