[Link](https://www.cloudflare.com/zh-cn/learning/network-layer/ipsec-vs-ssl-vpn/)


### IPsec VPN 与 SSL VPN：有何区别？
#### OSI 模型层

SSL 和 IPsec 之间的主要区别之一是各自属于 OSI 模型的哪一层。OSI 模型是一种抽象表示，将使互联网工作的进程细分为“层”。

IPsec 协议套件在 OSI 模型的网络层运作。它直接在 IP（互联网协议）的上方运行，后者负责路由数据包。

同时，SSL 在 OSI 模型的应用程序层运作。它对 HTTP 流量进行加密，而不是直接对 IP 数据包进行加密。

#### 实施
IPsec VPN 通常需要在将使用 VPN 的所有用户电脑上安装 VPN 软件。用户必须登录并运行该软件，才能连接到网络并访问其应用程序和数据。

相比之下，所有 Web 浏览器都已支持 SSL（而大多数设备并未自动配置为支持 IPsec VPN）。用户可以通过他们的浏览器而不是通过专用的 VPN 软件应用程序连接到 SSL VPN，而无需 IT 团队提供太多额外的支持。（但是，这意味着非浏览器的互联网活动不受 VPN 保护。）
