# 网络底座：IP、端口、TCP/IP、HTTP/TLS

## IP 是机器地址

IP 是网络里的门牌号。目标网站看到的“用户 IP”，通常是最后一跳出口。

```text
203.0.113.10 = 入口 VPS 公网 IP
198.51.100.20 = 静态 ISP 代理 出口 IP
```

桌面端走链式代理时，网站看到 `198.51.100.20`。移动端走 VPS 直出时，网站看到 `203.0.113.10`。

相关：[[05-xray-routing#中转和落地]]

## 端口是服务入口

```text
IP = 这台机器在哪里
端口 = 这台机器上的哪个服务入口
```

常见端口：

```text
22   SSH
80   HTTP
443  HTTPS / TLS
```

示例 Xray 监听：

```text
203.0.113.10:443
```

端口号不决定协议。`443` 只是默认常用于 HTTPS，也可以承载 Xray Reality、Trojan、SSH 等服务。真正协议是什么，要看连接后双方说什么“语言”。

完整 TCP 连接通常由四元组确定：

```text
源 IP + 源端口 + 目标 IP + 目标端口
```

例如：

```text
本地设备:52341 -> 203.0.113.10:443
```

## TCP/IP 分层

```text
应用层:
HTTP、HTTPS、DNS、SSH、VLESS、SOCKS5、Shadowsocks

传输层:
TCP、UDP

网络层:
IP

链路层:
Wi-Fi、以太网、蜂窝网络、运营商链路
```

职责：

```text
IP:
把包送到哪个 IP

TCP:
建立可靠连接，处理顺序、重传、拥塞控制

UDP:
轻量数据报，低延迟，不保证可靠

应用协议:
连接建立后双方具体说什么话
```

比喻：

```text
IP = 收件地址
TCP = 快递签收、编号、丢件重发
TLS = 包裹上锁
HTTP/VLESS/SOCKS5 = 包裹里的业务单据
```

## HTTP、HTTPS、TLS

```text
HTTP:
明文网页通信

HTTPS:
HTTP + TLS

TLS:
连接加密、身份认证、防篡改
```

TLS 保护连接内容，比如网页路径、请求头、Cookie、表单、响应正文。但它不隐藏所有外层元数据，沿途仍可能看到源 IP、目标 IP、端口、连接时间和流量大小。

HTTPS 和代理加密是两层：

```text
用户设备 -> VPS:
VLESS Reality 保护

VPS -> 目标网站:
目标网站 HTTPS 保护
```

## 本地开发为什么也有 IP 和端口

本地 HTML 游戏预览常见地址：

```text
http://localhost:3000
http://127.0.0.1:5173
https://localhost:8443
```

这不是访问公网，而是本机 dev server 在 Mac 上开了服务入口：

```text
浏览器 -> 127.0.0.1:5173 -> 本机 dev server -> 读取 HTML/JS/CSS
```

地址范围：

```text
127.0.0.1 / localhost:
本机回环，只能自己访问自己

192.168.x.x / 10.x.x.x:
局域网地址

203.0.113.x:
公网地址
```

访问 `127.0.0.1` 本身不会出公网，也不需要外部 DNS。但 Chrome 后台服务、扩展、外部 CDN、统计脚本、WebRTC/STUN 仍可能额外联网。

