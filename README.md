# 代理网络基础扫盲

这是一套面向初学者和半懂不懂状态学习者的中文网络代理知识库。它用一个“桌面端 -> 入口 VPS -> 静态 ISP 出口”和“移动端 -> 入口 VPS 直出”的示例架构，把 IP、DNS、VPS、端口、TCP/IP、TLS、SOCKS5、Shadowsocks、VLESS Reality、Xray、mihomo、Clash Verge、Shadowrocket、TUN、链式代理、DNS/IPv6 泄漏和信任模型串起来讲清楚。

本仓库是公开教学版，不包含真实服务商名称、真实 IP、账号、密码、UUID、密钥、二维码或任何个人部署信息。示例 IP 使用文档保留地址段，例如 `203.0.113.0/24` 和 `198.51.100.0/24`。

## 阅读入口

从这里开始：

- [代理网络知识库索引](00-index.md)

推荐顺序：

1. [网络底座：IP、端口、TCP/IP、HTTP/TLS](01-network-basics.md)
2. [DNS：解析、调度、泄漏和缓存](02-dns.md)
3. [VPS：云服务器、合规和被墙](03-vps.md)
4. [代理协议：SOCKS5、Shadowsocks、VLESS、Reality](04-proxy-protocols.md)
5. [Xray：入站、出站、路由和链式代理](05-xray-routing.md)
6. [客户端：Clash Verge、mihomo、Shadowrocket、TUN](06-clients.md)
7. [泄漏与信任模型：谁能看到什么](07-leaks-trust.md)
8. [平台控制：Mac、iPhone、Network Extension](08-platforms.md)
9. [操作与排错：检测、日志、规则、IPv6](09-ops.md)
10. [术语表](99-glossary.md)

## 适合谁读

- 想理解代理、VPS、DNS、TUN、VLESS Reality 的普通用户
- 配过 Clash/Shadowrocket，但对底层概念似是而非的人
- 想区分正向代理、反向代理、SOCKS5、Shadowsocks、VLESS 的开发者
- 想知道“代理到底隐藏了什么、没隐藏什么”的学习者

## 不是什么

这不是机场推荐、节点分享、翻墙教程或规避平台规则指南。它只解释网络与代理系统的基础概念、架构边界和排错思路。

## 许可

内容可用于个人学习和非商业转载。转载时请保留来源链接。
