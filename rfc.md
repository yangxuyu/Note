# rfc



1. [rfc826 - An Ethernet Address Resolution Protocol](https://www.rfc-editor.org/rfc/rfc826)
    这个RFC 826，标题为 "An Ethernet Address Resolution Protocol -- or -- Converting Network Protocol Addresses to 48.bit Ethernet Address for Transmission"，定义了以太网的地址解析协议（ARP）。具体来说，它描述了如何将网络层地址（如IPv4地址）转换为以太网的48位物理地址（MAC地址），以便在局域网（LAN）中进行数据传输。

	ARP的工作原理如下：
    1. **请求**：当一个设备需要发送数据包到另一个设备时，它会广播一个ARP请求，询问目标设备的MAC地址。
    2. **响应**：目标设备收到请求后，会回复一个包含其MAC地址的ARP响应。
    3. **缓存**：发起请求的设备会将这个映射关系（IP地址到MAC地址）存储在本地的ARP缓存中，以便后续通信时直接使用。

	ARP是确保在以太网环境中正确寻址和传输数据的关键机制。


2. [rfc2784 - Generic Routing Encapsulation](https://www.rfc-editor.org/rfc/rfc2784)
	 GRE的这个协议很简短，就是规定了一个封装头，把一个网络数据包（ipv4、ipv6等)封装在另一个ip数据包(ipv4等）里，从而不同的网络协议在网络协议里传输。
	

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
	