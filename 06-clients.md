# 客户端：Clash Verge、mihomo、Shadowrocket、TUN

## Clash Verge 和 mihomo

```text
Clash Verge = 图形界面 / 配置管理
mihomo = 真正处理代理、DNS、规则、TUN 的核心
VLESS Reality = mihomo 连接 VPS 使用的协议
```

关系类似：

```text
Chrome = 程序
HTTPS = Chrome 访问网站的协议
```

对应：

```text
mihomo = 程序/内核
VLESS Reality = 远程代理协议
```

## Shadowrocket

Shadowrocket 是 iOS 上的代理客户端，通过 iOS VPN / Network Extension 接管流量。

移动端示例：

```text
Shadowrocket -> VLESS Reality -> 入口 VPS -> Internet
```

全局路由：

```text
配置:
按规则分流

代理:
所有流量走所选代理
```

验证和日常稳定使用时，通常建议选“代理”。

## TUN 是什么

TUN 是虚拟网卡模式。开启后，系统大部分流量会被接管到代理客户端。

```text
System Proxy = App 自觉遵守
TUN/VPN = 系统路由层强制接管
```

强度：

```text
浏览器代理 < 系统代理 < TUN/VPN
```

## TUN 不是绝对结界

普通 App 很难无视系统 TUN，但仍有例外：

```text
另一个 VPN / TUN 抢路由
Clash 规则本身设置 DIRECT
局域网、localhost、mDNS 直连
Apple 系统服务特殊路径
WebRTC 局域网候选
IPv6 未接管
ARP、DHCP、AirDrop、蓝牙等本地物理网络层
```

检查重点：

```text
不要同时开启两个 TUN/VPN 客户端
确认规则不是误 DIRECT
确认 DNS 检测没有本地 DNS
确认 IPv6 不泄漏
```

## 代理客户端、内核和协议

```text
App = 方向盘、仪表盘、配置界面
内核 = 发动机，处理流量
协议 = 发动机和远端服务器说话的语言
```

三端发动机：

```text
桌面端:
Clash Verge 背后的 mihomo

移动端:
Shadowrocket 自己的网络核心

Linux VPS:
Xray / xray-core
```

它们不是同一个程序，但都支持 VLESS Reality，所以能互通。

## 断裂点

```text
协议支持不完整
字段名不兼容
传输层不兼容
UDP 支持差异
DNS/TUN 能力不同
配置格式不同
平台限制
服务商接口有限
```

IP 不绑定某家，协议兼容就能互通；配置格式和平台能力才是常见断裂点。

