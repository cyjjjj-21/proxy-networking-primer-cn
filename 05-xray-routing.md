# Xray：入站、出站、路由和链式代理

## Xray 是什么

Xray 是跑在 VPS 上的 Linux 代理核心。它不是单一协议，而是多协议、多入站、多出站、多路由规则的代理平台。

它负责：

```text
接收客户端连接
验证用户
处理代理协议
按路由规则选择出站
把流量发往外网或下一个代理
```

## Xray 像代理交换机

示例 VPS 上：

```text
inbounds:
VLESS Reality 监听 443

outbounds:
static-isp-socks、direct、block

routing:
iPhone 用户走 direct
其他默认走 静态 ISP 代理
```

它像一个交换机：

```text
流量从哪里进来
验证是谁
判断要去哪里
选择哪条出口
把流量送出去
```

## Inbound

Inbound 是入站入口。

```text
监听 0.0.0.0:443
协议 vless
安全层 reality
允许多个 client UUID
```

Mac 和 iPhone 都连同一个 VPS 443 端口，但使用不同 UUID。

## Outbound

Outbound 是出站出口。

```text
static-isp-socks:
转发到 静态 ISP 代理 SOCKS5

direct:
VPS 自己直连外网

block:
丢弃流量
```

## Routing

Routing 是路由规则：

```text
如果用户是 ios-direct@bandwagon:
走 direct

其他用户:
走默认 outbound，也就是 静态 ISP 代理
```

这就是同一台 VPS 同时服务两种线路的原因：

```text
桌面端 -> 静态 ISP 代理
移动端 -> VPS direct
```

## 中转和落地

中转是流量经过但不是最终出口的节点。落地是目标网站看到的最终出口。

Mac：

```text
桌面端 -> 入口 VPS -> 静态 ISP 代理 -> Internet
```

```text
入口 VPS = 中转
静态 ISP 代理 = 落地
```

iPhone：

```text
移动端 -> 入口 VPS -> Internet
```

```text
入口 VPS = 落地
```

## 链式代理

链式代理就是代理后面再接代理：

```text
设备 -> VPS -> ISP 代理 -> 目标网站
```

好处：

```text
入口和出口分离
可以快速换出口
不同设备走不同出口
降低单点污染
```

代价：

```text
延迟更高
配置更复杂
任何一跳坏了都会影响链路
排错要分层看
```

