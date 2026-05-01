# 平台控制：Mac、iPhone、Network Extension

## Mac 更像通用计算机

macOS 不是 Linux，但有很强 Unix 血统：

```text
macOS = Darwin/XNU + BSD 用户空间 + Apple 图形和安全层
Linux = Linux kernel + GNU/其他用户空间 + 发行版生态
```

Mac 适合开发和网络调试：

```text
ssh 到 VPS
跑脚本
装 Homebrew
开本地服务
改 DNS / hosts
抓包
跑 Docker / 虚拟机
```

但 macOS 也有 Apple 控制层：SIP、Gatekeeper、公证、TCC、Sandbox、DriverKit、MDM 等。

## iPhone 更像受托管终端

iOS 的模型：

```text
App 沙盒隔离
后台能力受限
系统 API 受 entitlement 控制
全局网络能力需要 Network Extension
分发主要通过 App Store
```

它牺牲一些自由度，换取安全、隐私和一致体验。

## Network Extension

Network Extension 是 iOS/macOS 给网络类 App 的官方高权限通道。

Shadowrocket 关键能力：

```text
NEPacketTunnelProvider
```

流程：

```text
Safari / App 发起请求
-> iOS 网络栈
-> Network Extension / Packet Tunnel
-> Shadowrocket 内核处理
-> 直连或代理
-> VPS / 代理节点
```

没有 Network Extension，普通 App 通常只能管自己的流量。有了它，才能全机流量接管、DNS 接管、TUN/Packet Tunnel、按规则分流。

## 安全策略还是商业策略

两者都是。

```text
安全策略提供正当性
体验策略巩固一致性
商业策略获得平台控制力
```

安全收益：

```text
恶意 App 更难偷数据
后台滥用受限
系统完整性更强
支付和钥匙串更受控
```

商业控制：

```text
App Store 分发
支付通道
后台服务形态
系统 API 准入
第三方很难深度接管系统体验
```

## 自己写 Shadowrocket 类 App

核心代理功能可以端侧完成，不一定需要开发者云服务器。

```text
用户设备
-> App 本地代理核心
-> 用户自己的 VPS/节点
-> 目标网站
```

开发者提供 App、Network Extension、协议实现、规则引擎、DNS 处理、导入体验和 UI。用户提供 VPS、订阅、SOCKS5、VLESS Reality 等节点。

难点在于：

```text
Network Extension
VPN 权限
TUN 虚拟网卡
DNS 接管
后台稳定性
多协议内核集成
App Store 审核
隐私政策和长期维护
```

