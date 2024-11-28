# rfc



1. [rfc826 - An Ethernet Address Resolution Protocol](https://www.rfc-editor.org/rfc/rfc826)
    这个RFC 826，标题为 "An Ethernet Address Resolution Protocol -- or -- Converting Network Protocol Addresses to 48.bit Ethernet Address for Transmission"，定义了以太网的地址解析协议（ARP）。具体来说，它描述了如何将网络层地址（如IPv4地址）转换为以太网的48位物理地址（MAC地址），以便在局域网（LAN）中进行数据传输。

ARP的工作原理如下：
    1. **请求**：当一个设备需要发送数据包到另一个设备时，它会广播一个ARP请求，询问目标设备的MAC地址。
    2. **响应**：目标设备收到请求后，会回复一个包含其MAC地址的ARP响应。
    3. **缓存**：发起请求的设备会将这个映射关系（IP地址到MAC地址）存储在本地的ARP缓存中，以便后续通信时直接使用。

ARP是确保在以太网环境中正确寻址和传输数据的关键机制。


2. [rfc2784 - Generic Routing Encapsulation](https://www.rfc-editor.org/rfc/rfc2784)
RFC 2784，标题为 "Generic Routing Encapsulation (GRE)”，定义了一种通用的路由封装协议。GRE 是一种网络协议，用于将一种网络协议的数据包封装在另一种网络协议的数据包中，从而实现不同网络之间的通信。

以下是 RFC 2784 的主要内容：

    1. **GRE 协议**：GRE 允许将任意网络层协议（如 IPv4、IPv6、IPX 等）的数据包封装在另一个网络层协议（通常是 IP）的数据包中。
    2. **封装过程**：GRE 封装通过在原始数据包外添加一个 GRE 头部来实现。这个头部包含必要的信息，以便接收端能够正确解封装并处理数据包。
    3. **GRE 头部格式**：GRE 头部包括标志位、协议类型、校验和等字段，这些字段帮助确保数据包的完整性和正确性。
    4. **GRE 隧道**：GRE 隧道是在两个网络节点之间建立的逻辑连接，用于传输封装的数据包。隧道的两端需要配置相同的 GRE 设置，以确保数据包能够正确传输。
    5. **应用场景**：GRE 常用于 VPN（虚拟专用网络）、网络虚拟化、多协议标签交换（MPLS）等场景，以实现不同网络之间的安全通信。

总的来说，RFC 2784 提供了一种标准化的方法，使得不同网络协议的数据包可以通过 GRE 封装在 IP 网络中进行传输，从而提高了网络的灵活性和可扩展性。


3. [rfc1853 - Generic Routing Encapsulation](https://www.rfc-editor.org/rfc/rfc1853)


4. [rfc2637 - Generic Routing Encapsulation](https://www.rfc-editor.org/rfc/rfc2637)


5. [rfc2661 - Generic Routing Encapsulation](https://www.rfc-editor.org/rfc/rfc2661)
RFC 2661，标题为 "Layer Two Tunneling Protocol (L2TP)"，定义了第二层隧道协议（L2TP）。L2TP是一种网络协议，用于在互联网上封装和传输第二层数据包，如点对点协议（PPP）数据包。具体来说，它描述了如何通过IP网络建立和维护虚拟私有拨号网络（VPDN）连接。

以下是RFC 2661的主要内容：

1. **背景和目的**：介绍了L2TP的背景、设计目标和应用场景。
2. **协议定义**：详细说明了L2TP的协议结构、消息格式和交互过程。
3. **安全机制**：讨论了L2TP的安全特性，包括如何使用IPsec进行加密和认证。
4. **操作模式**：描述了L2TP的不同操作模式，如客户端-服务器模式和对等模式。
5. **兼容性和扩展性**：确保L2TP与其他相关协议的兼容性，并提供了扩展机制以适应未来的需求。

RFC 2661是网络安全领域的重要文档，特别是在需要通过不安全的公共网络（如互联网）传输敏感数据时，提供了详细的指导和规范。






6. [rfc793 - Generic Routing Encapsulation](https://www.rfc-editor.org/rfc/rfc793)





10. [rfc3954 -Cisco Systems NetFlow Services Export Version 9](https://www.rfc-editor.org/rfc/rfc3954)
