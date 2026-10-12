
> just for fun

## 目录

点击右上角的 **「目录」** 图标打开目录，获得更好的阅读体验。

## 内容
> **以下为内容**｜ 不定期更新

### 网络基础

1. [rfc826 - An Ethernet Address Resolution Protocol](https://www.rfc-editor.org/rfc/rfc826):
	ARP，地址解析协议。核心就一件事：把 IP 地址换成 MAC 地址。设备要发数据前，广播一个 ARP 请求问"谁的 IP 是 xxx，把你的 MAC 告诉我"，目标设备回一个 ARP 响应带上自己的 MAC，发起方把这个映射记到 ARP 缓存里，后面直接查缓存，不用每次广播。局域网里能不能找对设备、把包送到位，就靠它。

2. [rfc1180 - A TCP/IP Tutorial](https://datatracker.ietf.org/doc/html/rfc1180):
	TCP/IP 入门教程，面向网络管理员。从数据链路层一路讲到应用层，覆盖 IP 地址、子网掩码、路由、ARP、ICMP、TCP 连接和端口这些基础，还讲了 ping、traceroute、netstat 这些排障命令。想快速上手 TCP/IP 可以看这个。

### TCP 与拥塞控制

1. [rfc793 - Transmission Control Protocol (TCP)](https://www.rfc-editor.org/rfc/rfc793):
	TCP 的规范定义（1981），实现 TCP 都得照着它来。报文段里的字段（端口、序列号、确认号、标志位、窗口、校验和）、三次握手建连接、四次挥手断开、超时重传和滑动窗口这些可靠传输机制全在里面。后来被 RFC 9293 取代，但理解 TCP 还是得看它。

2. [rfc813 - Window and Acknowledgement Strategy in TCP](https://www.rfc-editor.org/rfc/rfc813):
	讲 TCP 的窗口和确认策略。核心就几件事：滑动窗口怎么管收发、ACK 什么时候发（立即确认、延迟确认、捎带确认）、缓冲怎么分配，还有怎么避免频繁发只更新窗口的小报文浪费带宽。跟 RFC 793 一脉相承。

3. [rfc879 - The TCP Maximum Segment Size and Related Topics](https://www.rfc-editor.org/rfc/rfc879):
	定义 TCP 的 MSS（最大报文段长度），就是单个 TCP 段最多带多少数据，不含 TCP 头。IPv4 下默认 536 字节（576 的最小重组缓冲减掉 40 字节头），通过 SYN 里的 MSS 选项协商，取双方较小的。设得够小能避免 IP 层分片，减少重组开销。

4. [rfc896 - Congestion Control in IP/TCP Internetworks](https://www.rfc-editor.org/rfc/rfc896):
	拥塞控制的早期经典。核心观点：拥塞导致丢包和重传，重传又加剧拥塞，恶性循环。还讲了愚蠢窗口综合症（SWS）——接收方通告小窗口、发送方还发小报文，纯浪费带宽。提出了慢启动的雏形，后来被 Van Jacobson 1988 系统化成慢启动和拥塞避免。

5. [rfc2581 - TCP Congestion Control](https://www.rfc-editor.org/rfc/rfc2581):
	把 Van Jacobson 1988 年的拥塞控制算法标准化，定义了四个核心算法：慢启动（cwnd 从 1 个 SMSS 开始，每收一个 ACK 加一个，指数涨到 ssthresh）、拥塞避免（超过 ssthresh 后每 RTT 线性加一个）、快速重传（收到 3 个重复 ACK 不等超时立即重传）、快速恢复（重传后 ssthresh 减半、cwnd 调到 ssthresh+3×SMSS）。取代 RFC 2001。

6. [rfc5681 - TCP Congestion Control](https://www.rfc-editor.org/rfc/rfc5681):
	RFC 2581 的更新版，现在是 TCP 拥塞控制的基础规范。四个算法不变，主要是把 SMSS 的使用和 cwnd 增长规则说得更精确，明确了 ACK 计数、空闲和恢复阶段 cwnd 的处理，减少实现歧义。取代 RFC 2581。

7. [rfc6582 - The NewReno Modification to TCP's Fast Recovery Algorithm](https://www.rfc-editor.org/rfc/rfc6582):
	NewReno，解决 Reno 快速恢复在多个报文段同时丢失时效率差的问题。Reno 一次只重传一个，还可能过早退出恢复；NewReno 在快速恢复期间收到 partial ACK 就立刻重传下一个未确认的段，并用 recover 变量标记恢复起点，避免误判。取代 RFC 3782。

8. [rfc2018 - TCP Selective Acknowledgment Options](https://www.rfc-editor.org/rfc/rfc2018):
	定义 SACK 选项。传统 TCP 只确认连续收到的数据，多段丢了只能靠超时重传；SACK 让接收方在 ACK 里带上已收到的非连续段的序列号范围，发送方就知道到底哪些丢了，只重传丢的那些。SYN 里用 SACK-Permitted 选项协商是否启用。

9. [rfc2883 - An Extension to the Selective Acknowledgment (SACK) Option for TCP](https://www.rfc-editor.org/rfc/rfc2883):
	SACK 的扩展，加了 D-SACK（Duplicate SACK）。接收方在 SACK 里报告重复收到的段（第一个块表示重复数据的范围），发送方就能判断是不是做了不必要的重传、ACK 是不是丢了、报文是不是被重排了，据此调整重传策略。

10. [rfc2988 - Computing TCP's Retransmission Timer](https://www.rfc-editor.org/rfc/rfc2988):
	定义 TCP 重传计时器（RTO）怎么算。用 RTT 采样维护 SRTT 和 RTTVAR 来算 RTO，重传后不更新采样（Karn 算法，避免确认歧义），每次重传 RTO 加倍（指数退避）。初始值 3 秒，下限 1 秒。取代 RFC 1122 里 RTO 计算的部分。

11. [rfc6298 - Computing TCP's Retransmission Timer](https://www.rfc-editor.org/rfc/rfc6298):
	RFC 2988 的更新版，现在算 RTO 都按它来。主要变化：初始值从 3 秒改成 1 秒，取消了 1 秒的下限，允许更小的 RTO 适应高速网络。SRTT/RTTVAR、Karn 算法、指数退避这些核心机制保留。

### 隧道与 VPN

1. [rfc2784 - Generic Routing Encapsulation](https://www.rfc-editor.org/rfc/rfc2784):
	GRE（通用路由封装）很简单，就是规定了一个封装头，把一种网络层协议的数据包（IPv4、IPv6等）封装进另一种网络层协议的数据包（通常是IPv4）里，让不同网络协议能在现有网络上传输，也是隧道技术的基础。GRE头固定 4 字节，带校验和、路由、密钥、序列号几个标志位和协议类型字段，后面可以跟校验和、密钥、序列号这些可选字段。它不提供加密和认证，安全得靠 IPsec（GRE over IPsec），优点是开销小、能封装多种协议，常用于 VPN 隧道、IPv6 over IPv4、组播 over 单播。

2. [rfc1853 - IP in IP Tunneling](https://www.rfc-editor.org/rfc/rfc1853):
	IP-in-IP 隧道，最简单的隧道方式。把整个 IP 包塞进另一个 IP 包（外层头+内层头），发送端封装、接收端解封装，中间网络只按外层头转发。用于移动 IP、组播隧道、VPN 这些场景。实现简单开销小，但不加密，安全得靠 IPsec。

3. [rfc2637 - Point-to-Point Tunneling Protocol (PPTP)](https://www.rfc-editor.org/rfc/rfc2637):
	PPTP，微软主导的 VPN 隧道协议。基于 PPP，用 GRE 封装 PPP 帧当数据隧道，另开 TCP 1723 端口维护控制连接。支持 PAP/CHAP/MSCHAP 认证和 MPPE 加密。安全性比较弱，现在基本被 L2TP/IPsec、WireGuard 取代了。

4. [rfc2661 - Layer Two Tunneling Protocol (L2TP)](https://www.rfc-editor.org/rfc/rfc2661):
	L2TP，第二层隧道协议。用来在 IP 网上封装传输第二层数据包（比如 PPP），典型场景是拨号 VPN（VPDN）——远程用户通过它接入企业内网。它本身不加密，通常跟 IPsec 配合（L2TP/IPsec）提供认证和加密。比起 PPTP，L2TP 更标准、兼容性更好，是现在主流的远程接入 VPN 方案。

### HTTP

1. [rfc7230 - Hypertext Transfer Protocol (HTTP/1.1): Message Syntax and Routing](https://www.rfc-editor.org/rfc/rfc7230.html):
	HTTP/1.1 的报文语法和路由。报文长什么样（请求行/状态行、头部、消息体），keep-alive 持久连接和管线化，代理、网关、隧道怎么转发，还有 chunked 传输编码。跟 7231-7235 一起取代了 RFC 2616。

2. [rfc7231 - Hypertext Transfer Protocol (HTTP/1.1): Semantics and Content](https://www.rfc-editor.org/rfc/rfc7231.html):
	HTTP 的语义和内容表示。各种请求方法（GET/POST/PUT/DELETE 等）的语义和幂等性，1xx-5xx 状态码，媒体类型、字符集、语言这些表示元数据和内容协商。

3. [rfc7232 - Hypertext Transfer Protocol (HTTP/1.1): Conditional Requests](https://www.rfc-editor.org/rfc/rfc7232.html):
	HTTP 条件请求。用 ETag（分强弱）和 Last-Modified 当验证器，配合 If-Match、If-None-Match、If-Modified-Since 这些条件头，做缓存再验证、断点续传、乐观并发控制（412）。

4. [rfc7233 - Hypertext Transfer Protocol (HTTP/1.1): Range Requests](https://www.rfc-editor.org/rfc/rfc7233.html):
	HTTP 范围请求。用 Range 头请求指定字节范围（如 bytes=0-1023），服务器返回 206 Partial Content 和 Content-Range，支持多范围（multipart/byteranges）和 If-Range 条件范围。断点续传、视频拖动播放都靠它。

5. [rfc7234 - Hypertext Transfer Protocol (HTTP/1.1): Caching](https://www.rfc-editor.org/rfc/rfc7234.html):
	HTTP 缓存。分私有缓存（浏览器）和共享缓存（代理/CDN），用 Cache-Control（max-age、no-cache、no-store 等）和 Expires 控制，过期了再用 ETag/Last-Modified 回源验证。

6. [rfc7235 - Hypertext Transfer Protocol (HTTP/1.1): Authentication](https://www.rfc-editor.org/rfc/rfc7235.html):
	HTTP 认证框架。服务器用 401 + WWW-Authenticate 发起挑战，客户端用 Authorization 带凭据。支持 Basic 和 Digest 方案，还有代理认证（407、Proxy-Authenticate）。

7. [rfc7540 - Hypertext Transfer Protocol Version 2 (HTTP/2)](https://www.rfc-editor.org/rfc/rfc7540):
	HTTP/2。语义（方法、状态码、头部）跟 HTTP/1.1 兼容，但传输层整个重写了：二进制分帧、单连接多路复用（消除应用层队头阻塞）、流和优先级、服务端推送、配合 HPACK 压头部、流级流量控制。

8. [rfc7541 - HPACK: Header Compression for HTTP/2](https://www.rfc-editor.org/rfc/rfc7541):
	HPACK，HTTP/2 的头部压缩。静态表存常用头部用索引引用，动态表在连接期间维护增量更新，再加上 Huffman 编码和变长整数编码，把头部开销压下来。

### 网络安全

1. [rfc4301 - Security Architecture for the Internet Protocol](https://datatracker.ietf.org/doc/html/rfc4301):
	IPsec 的总体架构（2005，取代 RFC 2401）。提供机密性、完整性、源认证和防重放。核心是安全关联（SA）、SAD 和 SPD 三个数据库，协议用 AH（只认证）和 ESP（加密+认证），分传输模式和隧道模式，密钥由 IKE 协商。IPv4/IPv6 通用。

2. [rfc3173 - IP Payload Compression Protocol (IPComp)](https://datatracker.ietf.org/doc/html/rfc3173): 
	IP有效负载压缩协议，又名无损压缩，还名数据消冗余。主要内容其实很少，outbound压缩报文，inbound解压缩报文，IPv4/Ipv6报文头修改，IPComp头，安全是IPsec负责。

### 网络监控

1. [rfc3954 - Cisco Systems NetFlow Services Export Version 9](https://www.rfc-editor.org/rfc/rfc3954): 
	NetFlow v9 的流量导出格式。用模板（Template）灵活定义记录字段，新增字段不用改协议。导出报文是报文头+模板记录+数据记录的结构，支持 IPv4/IPv6、MPLS。后来 IPFIX（RFC 7011）就是基于它标准化的。






<p align="center">
    <!--
     <a href="https://github.com/521xueweihan/HelloGitHub/blob/master/content/HelloGitHub98.md">『上一期』</a> 
    -->
   | <a href='https://github.com/yangxuyu/Note/issues'>反馈和建议</a> |
    <!--
    <a href="https://github.com/521xueweihan/HelloGitHub/blob/master/content/HelloGitHub100.md">『下一期』</a>
    -->

</p>

---
