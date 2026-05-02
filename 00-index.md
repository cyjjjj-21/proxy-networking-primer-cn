# 代理网络知识库索引

更新时间：2026-05-01

这是一套以“自建 VPS + Xray + Clash Verge + 静态 ISP 代理”为主线的 Obsidian 风格笔记。这里主要解释概念、架构和排错，不包含真实服务商名称、真实 IP、账号、密码、密钥或二维码。

## 示例架构

```text
桌面端:
Clash Verge / mihomo -> 入口 VPS / Xray -> 静态 ISP 代理 SOCKS5 -> Internet

移动端:
Shadowrocket -> 入口 VPS / Xray -> Internet
```

## 推荐阅读顺序

1. [[01-network-basics|网络底座：IP、端口、TCP/IP、HTTP/TLS]]
2. [[02-dns|DNS：解析、调度、泄漏和缓存]]
3. [[03-vps|VPS：云服务器、合规和被墙]]
4. [[04-proxy-protocols|代理协议：SOCKS5、Shadowsocks、VLESS、Reality]]
5. [[05-xray-routing|Xray：入站、出站、路由和链式代理]]
6. [[06-clients|客户端：Clash Verge、mihomo、Shadowrocket、TUN]]
7. [[07-leaks-trust|泄漏与信任模型：谁能看到什么]]
8. [[08-platforms|平台控制：Mac、iPhone、Network Extension]]
9. [[09-ops|操作与排错：检测、日志、规则、IPv6]]
10. [[99-glossary|术语表]]

## 一句话心智模型

```text
DNS 把域名变成 IP
IP + 端口定位到某台机器上的某个服务
TCP 建立可靠连接
TLS/Reality 保护连接内容和外观
VLESS/SOCKS5 表达代理转发关系
Xray/mihomo/Shadowrocket 按规则调度流量
目标网站最终看到的是落地出口 IP
```

## 快速查找

- 想理解 DNS 为什么会变：[[02-dns#DNS 会看人下菜碟]]
- 想理解为什么本地 DNS 不能填根 DNS：[[02-dns#本地 DNS 设置应该填哪一层]]
- 想理解 VPS 为什么合法：[[03-vps#VPS 厂商为什么能合法存在]]
- 想理解被墙不等于自己做坏事：[[03-vps#VPS IP 被墙是什么意思]]
- 想理解为什么前半段用 VLESS、后半段用 SOCKS5：[[04-proxy-protocols#为什么示例前半段用 VLESS 后半段用 SOCKS5]]
- 想理解反向代理 Token 骗局：[[04-proxy-protocols#反向代理和 Token 骗局]]
- 想理解反代和正代的信息差：[[04-proxy-protocols#为什么第三方反代更像“骗用户信任”正向代理更像“隐藏用户来源”]]
- 想理解正代/反代为什么不是完美镜像：[[04-proxy-protocols#更底层的不对称：请求边本来就是单向的]]
- 想理解 Xray 是不是交换机：[[05-xray-routing#Xray 像代理交换机]]
- 想理解 Clash 规则是否合理：[[09-ops#示例 Clash 规则为什么合理]]
- 想理解 TUN 是否能兜住一切：[[06-clients#TUN 不是绝对结界]]
- 想理解 VPS 是否是信任点：[[07-leaks-trust#VPS 是核心信任点]]
- 想理解不可信中转为什么危险：[[07-leaks-trust#不可信中转能看到什么]]
- 想理解本地 dev server 为什么也有 IP 和端口：[[01-network-basics#本地开发为什么也有 IP 和端口]]
- 想理解 IPv6 怎么防漏：[[07-leaks-trust#IPv6 泄漏]]
- 想理解 VPS IP 被墙不等于自己做坏事：[[03-vps#VPS IP 被墙是什么意思]]
