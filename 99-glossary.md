# 术语表

```text
IP:
网络地址，目标网站看到的是最终出口 IP。

DNS:
域名解析系统，把域名变成 IP。

递归 DNS:
普通用户配置的 DNS，负责一路查询到底。

权威 DNS:
具体域名的真实记录管理者。

VPS:
租来的远程 Linux 服务器。

端口:
同一台机器上的服务入口编号。

TCP:
可靠连接协议。

UDP:
轻量数据报协议。

TLS:
加密连接层。

HTTPS:
HTTP + TLS。

SNI:
TLS 握手里的目标域名提示。

SOCKS5:
通用代理协议，适合做落地代理接口。

正向代理:
站在客户端一侧，替用户访问目标服务。

反向代理:
站在服务器一侧，替后端服务接收用户请求。

Shadowsocks:
轻量加密代理协议。

VLESS:
Xray 生态里的代理协议，负责表达代理请求语义，常搭配 TLS/Reality 等安全传输层。

Reality:
Xray 的 TLS 伪装与认证方案。

Xray:
VPS 上的代理核心，负责入站、出站、路由。

mihomo:
Clash 系代理核心，Clash Verge 背后的发动机。

Clash Verge:
Mac 上的图形代理客户端。

Shadowrocket:
iOS 上的代理客户端。

TUN:
虚拟网卡模式，系统路由层接管流量。

System Proxy:
系统代理设置，依赖 App 遵守。

Inbound:
Xray 入站入口。

Outbound:
Xray 出站出口。

Routing:
Xray 分流规则。

中转:
流量经过但不是最终出口的节点。

落地:
目标网站看到的最终出口。

静态 ISP IP:
看起来像固定 ISP/商业宽带的代理出口。

DNS 泄漏:
网页走代理，但 DNS 从真实本地网络出去。

IPv6 泄漏:
IPv4 走代理，但 IPv6 从真实本地网络出去。
```
